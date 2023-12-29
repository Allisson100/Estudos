# Criando rotas

Instalamos o nodemon:

    npm i nodemon

Criamos rotas de uma maneira diferente:

    import http from 'http'

    const PORT = 3000

    const rotas = {
        '/': 'Curso de Node.js',
        '/livros': 'Entrei na rota Livros',
        '/autores': 'Entrei na rota autores'
    }

    const server = http.createServer((req, res) => {
        res.writeHead(200, { 'Content-Type': 'text/plain' })
        res.end(rotas[req.url])
    })

    server.listen(PORT, () => {
        console.log('Server running!')
    })

Criamos um objeto com diversas rotas diferentes e nós mandamos uma mensagem de acordo com a rota com que o usuário utilizou, exemplo:

Se ele acessar a rota '/livros', o servidor vai obter essa rota através do req.url e a nossa função res.end() ficará assim:

    res.end(rotas['/livros'])

E isso é uma forma de obter um dado dentro de um objeto, ou seja, essa maneira irá nos retornar a string 'Entrei na rota Livros'.