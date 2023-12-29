# Buscas por parâmetro

Criamos uma rota para fazer buscas no banco de dados atrvés de parâmetros na url/rota:

Arquivo livroROutes.js:

    routes.get('/livros', LivroController.listarLivros)
    routes.get('/livros/busca', LivroController.listarLivrosPorEditora)
    routes.get('/livros/:id', LivroController.listarLivroPorId)

Coloquei essa três rotas para enfatizar que o express trabalhar como se fosse um hierarquia de rotas, então caso a rota '/livros/busca' estiver depois da rota '/livros/id', a rota busca não vai funcionar, pois a aplicação vai enterr que busca é um id.

Arquivo livroController:

    static async listarLivrosPorEditora (req, res) {

        const editora = req.query.editora

        try {

            const livrosPorEditora = await livro.find({ editora: editora })
            res.status(200).json(livrosPorEditora)
            
        } catch (erro) {
            res.status(500).json({
                message: `${erro.message} - Falha na busca do livro`
            })
        }
    }

Método listarLivrosPorEditora pega através da cont editora nosso parâmetro.

Lembrando que nossa url tem que ir assim:

    http://localhost:3000/livros/busca?editora=Rocco

Então o método entra na rota busca e entende que o valor de req.query.editora nesse caso é igual a Rocco.

Depois disso utilizamos o método find com o valor da editora lá dentro, lembrando que podemos escrever assim:

    const livrosPorEditora = await livro.find({ editora })

Pois os nomes são iguais, mas deixei com duas vezes editora para melhor interpretação.

E com isso retornamos como resposta um json com o objeto livro.



