# Ordenando os resultados

Aqui melhoramos a prte de ordenar os livros:

    static listarLivros = async (req, res, next) => {
        try {

            let { limite = 5, pagina = 1, ordenacao = "_id:-1" } = req.query;

            let [ campoOrdenacao , ordem ] = ordenacao.split(":");

            limite = parseInt(limite);
            pagina = parseInt(pagina);
            ordem = parseInt(ordem);

            if (limite > 0 && pagina > 0) {
                const livrosResultado = await livros.find()
                    .sort({ [campoOrdenacao]: ordem })
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

Dessa forma conseguimos passar os parâmtros de ordenação. Podemos escolher qual campo a gente quer levar em consideração e se queremos na ordem crescente ou decrescente.
