# Aplicando regex na busca

Aqui apenas melhoramos nossa busca:

    static listarLivroPorFiltro = async (req, res, next) => {
        try {
            const { editora , titulo } = req.query;

            const busca = {};

            if(editora) busca.editora = editora;
            if(titulo) busca.titulo = { $regex: titulo, $options: "i" };
        
            const livrosResultado = await livros.find(busca);

            res.status(200).send(livrosResultado);
        } catch (erro) {
            next(erro);
        }
    };

Basicamente utilizamos o regex, isso funcionaria tanto um regex do proprio javascript como o método $regex que o mongoose disponibiliza para nós.

Dessa forma o filtro por titulo pode conter por exemplo, 'arr', dessa forma ele vai retornar todos os titulo que contem as letras arr juntas idependente do titulo do livro. E a a prte de $options serve para definir que as letrar maiusculas e minusculas não sao diferentes, então 'M' e 'm' são a mesma coisa para a busca no banco de dados.