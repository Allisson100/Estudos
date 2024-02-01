# PaginandoUmaRota

Nessa parte arrumamos a parte de paginação da rota, no método listar litros fizemos o seguinte:

    static listarLivros = async (req, res, next) => {
        try {

            let { limite = 5, pagina = 1 } = req.query;

            limite = parseInt(limite);
            pagina = parseInt(pagina);

            if (limite > 0 && pagina > 0) {
                const livrosResultado = await livros.find()
                    .skip((pagina - 1) * limite)
                    .limit(limite)
                    .populate("autor")
                    .exec();

                res.status(200).json(livrosResultado);
            } else {
                next(new RequisicaoIncorreta());
            }

        } catch (erro) {
            next(erro);
        }
    };

criamos uma lógica para que através do parâmetros da rota possamos buscar apenas 5 itens do banco de dados e também com o skip podemos sempre pular uma quantidade de páginas o que da a ideia de paginação no site.