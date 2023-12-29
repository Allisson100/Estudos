# Unindo livros e autores

Criamos um novo schema para os autores e agora temos acrescentar os autores junto com os livros:

    static async cadastrarLivro (req, res) {

        const novoLivro = req.body

        try {

            const autorEncontrado = await autor.findById(novoLivro.autor)
            const livroCompleto = { ...novoLivro, autor: { ...autorEncontrado._doc } }

            const livroCriado = await livro.create(livroCompleto)
            
            res.status(201).json({
                message: 'Criado com sucesso',
                livro: livroCriado
            })

        } catch (erro) {
            res.status(500).json({
                message: `${erro.message} - Falha ao cadastrar livro`
            })
        }
    }

No método cadastrarLivro fizemos uma modificação.

Primeiro salvamos o body. Depois com a const autorEncontrado = await autor.findById(novoLivro.autor), fazemos uma pesquisa na collection autores para saber qual é o autor referente aquele ID. Depois disso monstamos um novo objeto onde o campo autores terá seus dados de forma correta.

Nós tivemos que usar essa estrutura aqui:

    const livroCompleto = { ...novoLivro, autor: { ...autorEncontrado._doc } }

Pois não vem só as informações do autor da collection, para ter acesso aos dados temos que acessar o _doc, por isso fizemos isso aqui, autor: { ...autorEncontrado._doc }.

E dessa forma conseguimos linkar duas collections diferentes para criar o livro novo.