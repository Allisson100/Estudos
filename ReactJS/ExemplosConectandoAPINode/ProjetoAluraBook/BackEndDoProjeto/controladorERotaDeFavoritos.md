# Controlador e rota de favoritos

Criamos por fim a parte de rotas e controladores do Favorito:

Controladores:

    const { getTodosFavoritos, insereFavorito, deletaFavoritoPorId } = require('../servicos/favorito')

    function getFavoritos(req, res) {
        try {
            const livros = getTodosFavoritos()
            res.send(livros)
        } catch (error) {
            res.status(500)
            res.send(error.message)
        }
    }

    function postFavorito(req, res) {

        try {
            const id = req.params.id

            insereFavorito(id)
            res.status(201)
            res.send('Livro inserido com sucesso!')
        } catch (error) {
            res.status(500)
            res.send(error.message)
        }
    }

    function deleteFavorito(req, res) {
        try {

            const id = req.params.id

            if (id && Number(id)) {

                deletaFavoritoPorId(id)
                res.send('Favorito deletado com sucesso!')

            } else {
                res.status(422)
                res.send('Id inválido')
            }

        } catch (error) {
            res.status(500)
            res.send(error.message)
        }
    }

    module.exports = {
        getFavoritos,
        postFavorito,
        deleteFavorito,
    }

Ai estão as funções que salva, insere e deleta os itens no banco de dados.

Rotas:

    const { Router } = require("express")
    const { getFavoritos, postFavorito, deleteFavorito } = require("../controladores/favorito")

    const router = Router()

    router.get('/', getFavoritos)

    router.post('/:id', postFavorito)

    router.delete('/:id', deleteFavorito)

    module.exports = router

E as respectivas rotas.

No nosso app.js temos que acrescentar essas rotas:

    const express = require('express')
    const rotaLivro = require('./rotas/livros')
    const rotaFavorito = require('./rotas/favorito')
    const cors = require('cors')

    const app = express()
    app.use(express.json())
    app.use(cors({origin: '*'}))

    app.use('/livros', rotaLivro)
    app.use('/favoritos', rotaFavorito)


    const port = 8000

    app.listen(port, () => {
        console.log(`App running, port: ${port}`);
    })

Apenas exportamos o arquivo de rotas e acrescentamos o código:

    app.use('/favoritos', rotaFavorito)