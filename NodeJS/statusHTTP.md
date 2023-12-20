# Status HTTP

Para saber os status de uma requisição existe um site que pode ajudar:

    https://httpstatusdogs.com

Forçamos um cenário de erro para entendermos como funciona

Arquivo livros.js:

    const { Router } = require('express')

    const router = Router()

    router.get('/', (req, res) => {

        try {

            throw new Error('teste')
            res.send('Olá Mundo!')

        } catch (error) {
            res.status(500)
            res.send(error.message)
        }

        
    })

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

Fizemos um try catch na rota .get e logo no try já lançamos um new Error para justamente forçar o erro.

E no catch nós falamos que tipo de erro é esse e também enviamos como resposta a mensagem de erro que nesse caso era 'teste'

