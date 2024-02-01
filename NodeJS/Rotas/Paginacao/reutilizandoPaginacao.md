# Reutilizando paginação

Agora nós criamos a parte de paginação como um middleware. Dentro da pasta middlewares criamos um arquivo chamado paginar.js:

    import RequisicaoIncorreta from "../erros/RequisicaoIncorreta.js";

    async function paginar(req, res, next) {

        try {
            let { limite = 5, pagina = 1, ordenacao = "_id:-1" } = req.query;

            let [ campoOrdenacao , ordem ] = ordenacao.split(":");

            limite = parseInt(limite);
            pagina = parseInt(pagina);
            ordem = parseInt(ordem);

            const resultado = req.resultado;

            if (limite > 0 && pagina > 0) {
                const resultadoPaginado = await resultado.find()
                    .sort({ [campoOrdenacao]: ordem })
                    .skip((pagina - 1) * limite)
                    .limit(limite)
                    .exec();

                res.status(200).json(resultadoPaginado);
            } else {
                next(new RequisicaoIncorreta());
            }
        } catch (erro) {
            next(erro);
        }
    }

    export default paginar;

E agora podemos adiconar esse middleware em rotas especificas:

    .get("/livros", LivroController.listarLivros, paginar)
    .get("/livros/busca", LivroController.listarLivroPorFiltro, paginar)

Como podemos ver tanto a rota '/livros' como a rota '/livros/busca' utilização o conceito de paginação, mas para que isso funcione devemos arrumar nosso código nos controllers também:


    static listarLivros = async (req, res, next) => {
        try {
            const buscarLivros = livros.find();
            req.resultado = buscarLivros;
            next();

        } catch (erro) {
            next(erro);
        }
    };

Aqui por exemplo nós tiramos o await do código, pois agora estamos meio que armazenando essa pesquisa para passar ao middleware e ele fazer essa pesqiusa para gente. E também armazenamos isso em req.resultado e obtemos ele na const resultado = req.resultado da função paginar. E não podemos esquecer do next(), pois é ele que faz com que a requisição passe para o próximo middleware que está ligado com aquela rota.

Todos os métodos de controller que utilizar o middleware paginar deve alterar o código para armazenar a busca em req.resultado.