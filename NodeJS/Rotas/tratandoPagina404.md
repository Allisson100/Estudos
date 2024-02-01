# Tratando página 404

Tratamos o erro 404 que é quando uma rota não é encontrada.

Primeiros no arquivo app.js:

    import express from "express";
    import db from "./config/dbConnect.js";
    import routes from "./routes/index.js";
    import manipuladorDeErros from "./middlewares/manipuladorDeErros.js";
    import manipulador404 from "./middlewares/manipulador404.js";

    db.on("error", console.log.bind(console, "Erro de conexão"));
    db.once("open", () => {
        console.log("conexão com o banco feita com sucesso");
    });

    const app = express();
    app.use(express.json());
    routes(app);

    app.use(manipulador404);
    app.use(manipuladorDeErros);

    export default app;

Criamos o app.use(manipulador404);

Dentro de middlewares criamos um arquivo chamado manipulador404.js e nele digitamos:

    import NaoEncontrado from "../erros/NaoEncontrado.js";

    function manipulador404 (req, res, next) {
        const erro404 = new NaoEncontrado();
        next(erro404);
    }

    export default manipulador404;

Aqui primeiro pegamos esse erro como a const erro404. E também criamos uma classe para NaoEncontrado:

    import ErroBase from "./ErroBase.js";

    class NaoEncontrado extends ErroBase {
        constructor(mensagem = "Pagina não encontrada") {
            super(mensagem, 404);
        }
    }

    export default NaoEncontrado;

E com isso através do next podemos jogar o erro para nosso manipulador de error e ele ira definir qual mensagem de erro deve aparecer:

    import mongoose from "mongoose";
    import ErroBase from "../erros/ErroBase.js";
    import RequisicaoIncorreta from "../erros/RequisicaoIncorreta.js";
    import ErroValidacao from "../erros/ErroValidacao.js";
    import NaoEncontrado from "../erros/NaoEncontrado.js";

    // eslint-disable-next-line no-unused-vars
    function manipuladorDeErros(erro, req, res, next) {
        if(erro instanceof mongoose.Error.CastError) {
            new RequisicaoIncorreta().enviarResposta(res);
        } else if (erro instanceof mongoose.Error.ValidationError) {
            new ErroValidacao(erro).enviarResposta(res);
        } else if (erro instanceof NaoEncontrado) {
            erro.enviarResposta(res);
        } else {
            new ErroBase().enviarResposta(res);
        }
    }

    export default manipuladorDeErros;

E dentro do nossos controllers, os método que utilizam ID ficam dessa forma:

    static atualizarAutor = async (req, res, next) => {
        try {
            const id = req.params.id;
  
            const autorResultado = await autores.findByIdAndUpdate(id, {$set: req.body});

            if (autorResultado !== null) {
                res.status(200).send({message: "Autor atualizado com sucesso"});
            } else {
                next(new NaoEncontrado("Id do Autor não localizado."));
            }

        } catch (erro) {
            next(erro);
        }
    };

    static excluirAutor = async (req, res, next) => {
        try {
            const id = req.params.id;

            const autorResultado = await autores.findByIdAndDelete(id);


            if (autorResultado !== null) {
                res.status(200).send({message: "Autor removido com sucesso"});
            } else {
                next(new NaoEncontrado("Id do Autor não localizado."));
            }
        } catch (erro) {
            next(erro);
        }
    };

Prmeiro analisamos se o a busca com o id que veio pela url é valida, se não for nós jogamos um erro com o next e passamos a mensagem daquele erro.