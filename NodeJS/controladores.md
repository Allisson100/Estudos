# Controladores

O router tem a resposabilidade apenas de direcionar o usuário pelas rotas, a questão de lógica podemos deixar a cargo dos controladores.

Então criamos uma pasta dentro de alura-books-server chamada controladores e dentro dela criamos um arquivo com o mesmo nome das rotas, ou seja, já que queremos criar controladores para o conjunto de rotas do arquivos livros.js, então dentro da nossa pasta controladores vamos criar um arquivo chamado livros.js também.

Então no nosso arquivo livros.js da pasta controladores:

    function getLivros (req, res) {
        try {
            res.send('Olá Mundo!')
        } catch (error) {
            res.status(500)
            res.send(error.message)
        }
    }

    module.exports = {
        getLivros
    }

Criamos uma função que vai receber o req e res. É claro que por enquanto o nome da função está genérico.

E depois não podemos esquecer de exportá-la, mas lembrando de exportar como objeto, pois depois terá mais funções.

No arquivo livros.js da pasta rotas fica dessa forma:

    const { Router } = require('express')
    const { getLivros } = require('../controladores/livros')

    const router = Router()

    router.get('/', getLivros)

    router.post('/', (req, res) => {
        res.send('Você fez uma requisição do tipo POST.')
    })

    router.patch('/', (req, res) => {
        res.send('Você fez uma requisição do tipo PATCH.')
    })

    router.delete('/', (req, res) => {
        res.send('Você fez uma requisição do tipo DELETE.')
    })

    module.exports = router

Como podemos ver, importamos a função e utilizamos ela na rota .get.

