# Rotas de post, patch e delete

- Post: inserir dados
- Delete: deletar dados
- Patch: editar dados

Vamos utilizar o Postman.

### Postman

No aplicativo do Postaman criamos um nova collection e clicamos em request.

E colocamos nossa url lá no input:

    http://localhost:8000/livros

Criamos alguns exmplos para saber os tipos basicos de requisição que existem.

Arquivo livros.js :

    const { Router } = require('express')

    const router = Router()

    router.get('/', (req, res) => {
        res.send('Olá Mundo!')
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

