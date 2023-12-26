# Ativando o modo hacker / Depurando métodos HTTP / Configurando cabeçalhos para autenticar o usuário / Depurando os códigos resposta HTTP

## Anotações Unidade 03

## Aula 01 (Ativando o modo hacker)

Telnet cria conexões TCP com outros servidores.

O formato das mensagens HTTP:

Envio:

    POST /public/login HTTP/1.1 // Linha Inciial

    Host: localhost //
    Content-Type: application/json // cabeçalhos (headers)
    Content-length: 45 //

    {'email': 'geo@alura.com.br', 'senha': '123'} //corpo(body)

Resposta:

    HTTP/1.1 200 OK // Linha Inciial

    X-Powered-By: Express //
    Vary: Origin, Accept-Encoding // cabeçalhos (headers)
    (...)
    Content-Type: application/json
    Content-length: 364 //

    {
        'access_token': 'dcvbdcsKJHDB...hdsbhsdbh'     
    } //corpo(body)

## Aula 02 (Depurando métodos HTTP)

Os principais métodos do HTTP

- POST: criar(create)
- GET: ler(read)
- PUT: atualizar(update)
- DELETE: apagar(delete)

## Aula 03 (Configurando cabeçalhos para autenticar o usuário)

Servidores HTTP são steteless, ou seja, eles não lembram o que aconteceu antes, não guarda estado.

Se a gente quiser acessar a lista de pedidos de um usuário pelo Postman, precisamos fazer uma configuração específica, pois o normal é que cada usuário tenha sua própria lista de pedidos.

Primeiro temos que fazer o login enviando pelo body os dados de login e senha e o método POST, pois dessa forma vamos criar um access-token.

Depois copiamos esse token que foi gerado no login e vamos na aba de Headers do Postman e colocamos Authorization no campo KEY  e no value colocamos a palavras Bearer espaço crtl V no token de acesso.

Sabemos que o HTTP é stateless, mas temos algumas formas de fazer ele lembrar. Uma das formas é por sessão, que foi o que fizemos no Postman, que no caso geramos um token e com esse token tivemos acesso aos nosso dados.

E temos o Cookie que é um mecanismo do HTTP que é utilizado nos Headers do HTTP para que o servidor peça ao usuário que o servidor salve algumas informações que vão ser utilizadas depois para que o servidor HTTP lembre dele depois.

- Sessão: tempo que o usuário passa logado
- Cookie: mecanismo para armazenar dados do cliente.

## Aula 04 (Depurando os códigos resposta HTTP)

Vimos o documento RFC que nos mostra os significados de todos os códigos que o servidor nos retorna. Ali tem todas as regras do protocolo HTTP.
