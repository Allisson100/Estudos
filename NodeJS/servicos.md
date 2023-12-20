# Criando serviços

Da mesma forma que as rotas não tem a responsabilidade de criar lógica, os controladores também não tem a responsabilidade de se conectar com ambientes externos, por exemplo um banco de dados.

No nosso caso estamos apenas lendo um JSON, mas isso é como se fosse a simulação de um banco de dados.

Então criamos uma nova pasta na raiz do projeto chamada servicos e dentro dela um arquivo chamado livros.js e nele digitamos:

    const fs = require('fs')

    function getTodosLivros() {
        return JSON.parse(fs.readFileSync('livros.json'))
    } 

    module.exports = { getTodosLivros }

Ele apenas retorna todos os livros que tem no nosso arquivo que estamos simulando como um banco de dados.

Vale lembrar que isso é importante, pois os controladores não tem que saber de que forma vamos nos concetar com o banco de dados, podemos até no funturo mudar o banco que utilizamos de forma simples, pois está tudo sperado de forma organizada.