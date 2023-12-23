# Criando serviço de livros

Criamos dentro de src uma pasta chamada servicos que será onde vamos fazer nossas requisições. Dentro dela criamos um arquivo chamado livros.js e nele digitamos:

    import axios from 'axios'

    const livrosApi = axios.create({
        baseURL: 'http://localhost:8000/livros'
    })

    function getLivros() {
        const response = livrosApi.get('/')

        return response.data
    }

    export {
        getLivros,
    }

Utilizamos o axios e criamos uma instancia dele com a const livrosApi.

Após isso podemos utilizar o métodos get, delete, etc para fazer as quisições para as rotas necessárias.

Nesse primeiro caso apenas criamos uma função chamada getLivros onde vamos fazer uma requisição do tipo get para a rota / da rota /livros, pois foi dessa forma que criamos lá no servidor node.

E depois apenas exportamos essa função.

