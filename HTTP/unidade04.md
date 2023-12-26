# Protegendo nossa aplicação com HTTPS / Entendendo certificados e chaves privadas

## Anotações Unidade 04

## Aula 01 (Protegendo nossa aplicação com HTTPS)

Wireshark é um programa que fica observando tudo que fica passando pela rede do nosso computador para simular um ataque hacker.

A forma como estava o projeto da AluraBook fez com que o wireshark conseguisse obter o nosso login e senha.

Então agora vamos testar utilizando o HTTPS e ver se realmente no traz mais segurança.

Utilizamos o openssl para isso.

Dentro da nossa pasta API digitamos um comando no terminal:

    openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout server.key -out server.crt

Isso faz com que se crie dois arquivos novos referente a essa segurança dentro da nossa pasta API.

Agora precisamos mudar o codigo do servidor, mais preciso onde nós abrimos o servidor, no nosso caso fica assim:

Ao invés de fazer somente:

    server.listen(8000, () => {
        console.log('APi disponível em http://localhost:8000')
    })

Vamos fazer o seguinte:

Primeiro importamos o https:

    const https = require('https')

    https.createServer(
        {
            key: fs.readFileSync('server.key')
            cert: fs.readFileSync('server.crt')
        },
        server
    ).listen(8000, () => {
        console.log('APi disponível em http://localhost:8000')
    })

Dessa forma o wireshark capita que fizemos alguma requisição porém os dados ficam embaralhados, ou seja, criptografados sendo impossíveis de ler.

## Aula 02 (Entendendo certificados e chaves privadas)

Com essa segunrança que criamos agora temos o seguinte fluxo com a segurança:

O cliente faz a requisição para o servidor, primeiro temos a troca de documentos, ou seja, o servidor envia o certificado para o cliente e o cliente envia um chave privada para servidor, isso serve para ter a troca de identificação e saber que estamos enviando e recebendo dados das pessoas certas vamos dizer assim.

Depois disso o cliente vai enviar a requisição e o algoritmo vai criptografar isso, o backend vai resolver essa criptografia, vai fazer o que o cliente pediu e vai enviar os dados dessa requisição de forma criptografada também.


