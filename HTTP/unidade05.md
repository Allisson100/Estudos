# Usando parâmetros com GET e POST / Configurando o formato dos dados

## Anotações Unidade 05

## Aula 01 (Usando parâmetros com GET e POST)

Passamos um parâmetro para a url:

    http://localhost:8000/livros?categoria=3

Utilizamos o ? para dizermos que queremos passar um parâmetro, depois o nome da variavel que no noss caso é categorias e depois o valor dessa variável que no caso é 3.

Isso utilizando o método GET.

Esses parâmetros se chama Query Params.

Já no post como já sabemos temos que enviar os dados pelo body, já que enviamos um JSON com diversos dados sobre o novo livro que queremos criar.

Lembrando que não existe limite de filtroes na URL.

E para passar mais de um filtro utilizamos o &.

Exexmplo:

    http://eletronicos.com/products?search=TV&maxPrice=1000&brand=ACME&model=XPTO&delivery=free&

## Aula 02 (Configurando o formato dos dados)

Criamos uma rota para que a equipe do front end consiga ter uma documentação da nossa API.

    server.get('/public/docs', (req, res) => {
        const meuHTML = `
            <h1>Documentação da API</h1>
            <ul>
                <li>GET /livros</li>
                <li>POST /livros</li>
                <li>GET /categorias</li>
            </ul>
        `

        res.status(200).contentType('text/html').send(meuHTML)
    })

Dessa forma essa rota vai enviar um arquivo HTML para o desenvolvedor front end.

O formato dos dados é definido pelo Content-Type:

- Content-type: formato do corpo da mensagem.
- Accept - usado na requisição.


