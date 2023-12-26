# Resolvendo algumas limitações do HTTP / Conhecendo o HTTP3

# Anotações Unidade 06

## Aula 01 (Resolvendo algumas limitações do HTTP)

HTTP/1.1 VS HTTP/2

HTTP/1.1:

- requisições sequenciais
- cabeçalhos textuais
- request obrigatório

HTTP/2:

- multiplexação
- compactação de cabeçalho
- server push (podemos configurar o servidor para que ele empurre os dados para o cliente mesmo sem ele pedir, pois já sabemos que ele vai utilizá-los no futuro, por exemplo imagens que tem em nosso site.)

Para utilizar o HTTP 2 temos que usar o https, pois ele já vem com a segunraça junto por ser uma versao mais recente do HTTP.

Temos que instalar a biblioteca que habilita o HTTP 2 no nosso projeto:

    npm i spdy

Vamos fazer o build do projeto também:

    npm run build

Depois vamos no nosso projeto da API.

Criamos um novo arquivo na raiz chamado server_http2.js e nele digitamos:

    const spdy = require('spdy')
    const express = require('express')
    const fs  = require('fs')

    const app = express()

    app.use(express.static('build'))

    spdy.createServer(
        {
            key: fs.readFileSync('./server.key'),
            cert: fs.readFileSync('./server.crt')
        },
        app
    ).listen(3002, (err) => {
        if (err) {
            throw new Error(err)
        }

        console.log('Listening on port 3002')
    })

E para rodar ele digitamos:

    node server_http2.js

## Aula 02 (Conhecendo o HTTP3)

HTTP/3(QUIC):

O HTTP 3 usa uma variação do UDP que se chama QUIC.

Ele ainda está em fase de testee ainda não temos todas as bibliotecas disponíveis para implementálo em todas as linguagens.

