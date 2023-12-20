# Lidando com parameters

Aprendemos a passar o id pelo a url.

Quremos buscar em nosso banco de dados apenas um livro e vamos buscá-lo através do id dele.

Então criamos uma nova função em serviços chamada getLivrosPorId(id) e passamos para ela o ide do livro em questão para conseguirmos buscá-lo no banco de dados.

    const fs = require('fs')

    function getTodosLivros() {
        return JSON.parse(fs.readFileSync('livros.json'))
    }

    function getLivrosPorId(id) {
        const livros = JSON.parse(fs.readFileSync('livros.json'))

        return livros.filter((livro) => livro.id === id)[0]
    }


    module.exports = { getTodosLivros , getLivrosPorId }

Criamos também uma função no controlador:

    function getLivro (req, res) {
        try {
            const id = req.params.id
            const livro = getLivrosPorId(id)
            res.send(livro)
        } catch (error) {
            res.status(500)
            res.send(error.message)
        }
    }

A const id utiliza o req.params.id para obter o id que está vindo daquela rota, mas vale lembrar que também acrescentamos uma rota nova:

    router.get('/:id', getLivro)

Agora lá no postman se escrevermos:

    http://localhost:8000/livros/1

A rota está passando para o controlador o id que po sua vez passa esse id através de parâmetro para a função getLivrosPorId que está fazendo a conexão com o banco de dados e buscando somente um livro através do id.

