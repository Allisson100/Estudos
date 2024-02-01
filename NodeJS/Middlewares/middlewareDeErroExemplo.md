# Middlewares do Express

Criamos um middleware para amanipular os erros de requisições em nossa aplicação.

Arquivo app.js:

    app.use(manipuladorDeErros);

Criamos também uma pasta chamada middlewares dentro de src e criamos um arquivo chamado manipuladorDeErros.js e nele digitamos:

    import mongoose from "mongoose";

    // eslint-disable-next-line no-unused-vars
    function manipuladorDeErros(erro, req, res, next) {
        if(erro instanceof mongoose.Error.CastError) {
            res.status(400).send({message: "Um ou mais dados fornecidos estão incorretos"});
        }else {
            res.status(500).send({message: "Erro interno de servidor."});
        }
    }

    export default manipuladorDeErros;

Basicamente aqui temos a função que trata o erro. Nesse caso temos apenas dois erros, um que é sobre o erro do mongoose em relaçoa ao ID e o outro é um erro mais genérico.

Para utilizar esse midleware que verifica se nossa aplicação tem algum erro, no arquivo livrosController.js e autoresController.js devemos colocar o next no catch, exemplo:

    static listarAutorPorId = async (req, res, next) => {

        try {
            const id = req.params.id;

            const autorResultado = await autores.findById(id);

            if(autorResultado !== null) {
                res.status(200).send(autorResultado);
            } else {
                res.status(404).send({message: "Id do Autor não localizado."});
            }
        } catch (erro) {
            next(erro);
        }
    };

Utilizamos o nerxt(erro) em todos os método dos controllers.



