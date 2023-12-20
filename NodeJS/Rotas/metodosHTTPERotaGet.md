# Métodos HTTP e rota get

O que são API?

Cliente - FrontEnd
Garçom - API

Rotas:

Ligação entre um método HTTP, uma URL e uam função.

### Código

Começamos a criar nossas rotas. Vale lembrar que esse curso é o backend do projeto frontend que fizemos anteriormente daAlurabooks.

Para melhor organização de rotas começamos criando dentro da pasta do projeto uma pasta chamada rotas e dentro dela criamos um arquivo chamado livros.js e nele digitamos:

    const { Router } = require('express')

    const router = Router()

    router.get('/', (req, res) => {
        res.send('Olá Mundo!')
    })

    module.exports = router

E nosso arquivo app.js ficou dessa forma:

    const express = require('express')
    const rotaLivro = require('./rotas/livros')

    const app = express()

    app.use('/livros', rotaLivro)


    const port = 8000

    app.listen(port, () => {
        console.log(`App running, port: ${port}`);
    })

O que criamos aqui.

Primeiro exportamos do express a função Router que serve justamente para nos ajudar nessa questão de rotas.

Depois atribuimos essa função à uma constante.

Criamos um rota inicial no arquivo livros.js , '/'. E nessa rota mudamos pedimos para que o servidor nos mande um console.log com uma mensagem.

Depois exportamos isso com module.exports = router.

No arquivo app.js fazemos o import desse conjunto de rotas e podemos dar um nome qualquer para ele que nesse caso foi rotaLivro.

Depois digitamos:

    app.use('/livros', rotaLivro)

Isso aqui quer dizer o que? Basicamente a rota '/' lá do arquivo livros.js se refere a rota '/livros', elas tão meio que linkadas e funciona desse jeito mais para facilidade e organização.





