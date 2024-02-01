# Filtrando por nome do autor

Criamos uma nova busca:

    static listarLivroPorFiltro = async (req, res, next) => {
        try {

            const busca = await processaBusca(req.query);
        
            const livrosResultado = await livros
                .find(busca)
                .populate("autor");

            res.status(200).send(livrosResultado);
        } catch (erro) {
            next(erro);
        }
    };

Criamos a função processaBusca():

    async function processaBusca(parametros) {
        const { editora , titulo , minPaginas , maxPaginas , nomeAutor } = parametros;

        const busca = {};

        if(editora) busca.editora = editora;
        if(titulo) busca.titulo = { $regex: titulo, $options: "i" };

        if(minPaginas || maxPaginas) busca.numeroPaginas = {};

        if(minPaginas) busca.numeroPaginas.$gte = minPaginas;
        if(maxPaginas) busca.numeroPaginas.$lte = maxPaginas;

        if(nomeAutor) {
            const autor = await autores.findOne({ nome: nomeAutor });
            const autorId = autor._id;

            busca.autor = autorId;
        }

        return busca;
    }

E adicionamos a possível busca nomeAutor.

Fizemos uma logica um pouco maior:

    if(nomeAutor) {
        const autor = await autores.findOne({ nome: nomeAutor });
        const autorId = autor._id;

        busca.autor = autorId;
    }

Isso porque a forma como nosso banco de dados foi modelado exige que nós precisamos passar o id do autor na hora da criação do livro e não o nome dele em si. Então primeiro buscamos o id do autor da busca e depois salvamos ele em nosso objeto busca.