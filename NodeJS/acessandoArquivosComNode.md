# Acessando arquivos com Node

Criamos um arquivo na raiz do projeto chamado livros.json. A ideia é simular nele dados de um banco de dados:

    [
        {
            "id": "1",
            "nome": "Livro irado" 
        },
        {
            "id": "2",
            "nome": "Livro muito legal" 
        }
    ]

Também criamos um arquivo chamado teste.js para testarmos algumas coias. Uma delas foi um maneira de ler um arquivo de nosso projeto com a função fs:

    const fs = require('fs')

    console.log(JSON.parse(fs.readFileSync('livros.json'))); 

Rodando no terminal node teste.js ele vai nos retornar nesse console.log() justamente o array de objetos presente no arquivo livros.json.

### Modificando o arquivo

Da mesma forma que podemos ler um arquivo, podemos também modificar esse mesmo arquivo da seguinte forma:

    const fs = require('fs')

    const dadosAtuais = JSON.parse(fs.readFileSync('livros.json'))

    const novoDado = {
        "id": "3",
        "nome": "Livro top" 
    }

    fs.writeFileSync('livros.json', JSON.stringify([...dadosAtuais, novoDado]))

Tivemos que criar uma contante para armazenar os dados atuais do arquivo e depois com a função writeFileSync() atrvés do spread operator acrescentamos os dados atuais somado com os dados novos que vem da const novoDado.