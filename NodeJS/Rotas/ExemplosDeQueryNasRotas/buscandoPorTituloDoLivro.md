# Buscando por título do livro

Começamos a implementar buscas em nossa aplicação. Em nosso arquivo livrosControllers.js mudamos o nome da função para listarLivrosPorFiltro e nela digitamos:

    static listarLivroPorFiltro = async (req, res, next) => {
        try {
            const { editora , titulo } = req.query;

            const busca = {};

            if(editora) busca.editora = editora;
            if(titulo) busca.titulo = titulo;
        
            const livrosResultado = await livros.find(busca);

            res.status(200).send(livrosResultado);
        } catch (erro) {
            next(erro);
        }
    };

Criamos um objeto dinâmico que consegue ter as propriedades corretas de acordo com os parâmetros que recebemos por string  e com isso passamos o obejto para o método find(), assim o mongodb consegue no retornar os itens correspondentes corretamente.