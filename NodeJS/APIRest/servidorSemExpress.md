# Criando o servidor

Começamos o projeto com:

    npm init

E adicionamos no package.json:

    "type": "module",

Agora criamos um servidor sem utilizar o expressa por enquanto:

    import http from 'http'

    const PORT = 3000

    const server = http.createServer((req, res) => {
        res.writeHead(200, { 'Content-Type': 'text/plain' })
        res.end('Curso de Node.Js')
    })

    server.listen(PORT, () => {
        console.log('Server running!')
    })

Nós utilizamos a biblioteca http para isso que já é nativa do Node e criamos um servidor com http.createServer().

Ele recebe um callback e dentro do callback temos outras duas funções, a res.writeHead() que nada mais é que o Header da requisição, então nós passamos o status e o tipo de dado que queremos trafegar.

Depois utilizamos o res.end() que seria o que nosso servidor deve responder e nesse caso passamos apenas uma mensagem padrão.

Por fim utilizamos o server.listen() para rodar o servidor.

