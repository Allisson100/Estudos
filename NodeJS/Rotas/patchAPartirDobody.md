# Patch a partir do body

Agora criamos uma forma de modificar algum item do nosso banco de dados.

Servicos:

    function modificaLivro(modificacoes, id) {

        let livroAtuais = JSON.parse(fs.readFileSync('livros.json'))

        const indiceModificado = livroAtuais.findIndex(livro => livro.id === id)

        const conteudoMudado = { ...livroAtuais[indiceModificado], ...modificacoes }

        livroAtuais[indiceModificado] = conteudoMudado

        fs.writeFileSync('livros.json', JSON.stringify(livroAtuais))
    }

Primeiro criamos nossa função modificaLivro que recebe dois parametros, as modificações e aqui pode ser qualuqer coisa, por exemplo, nós podemos dizer que queremos mudar apenas o nome do livro, podemos dizer que queremos mudar somente o nome do autor ou podemos dizer que queremos mudar um ou mais itens daquele objeto, por exemplo o nome do livro e do autor, então nossa função tem ser dinâmica dessa forma.

Então explicando melhor nossa função, primeiro pegamos todos os livros do banco de dados.

Depois nós pegamos o indice do livro que queremos modificar fazendo uma busca atrvés do id recebido, isso acontece através da função findIndex, onde nos retorna o indice do item de acordo com a condição que criamos atrvés do callback.

Sabendo o index do item, podemos utilizar o spread operator para fazer uma coisa muito interessante.

    const conteudoMudado = { ...livroAtuais[indiceModificado], ...modificacoes }

A const conteudoMudado funciona da seguinte forma:

- Primeiro ela recebe uma cópia do objeto livroAtuais[indiceModificado], depois ela pega o outro objeto que nesse caso é modificacoes e começa a comparar.

- Vamos supor que o objeto naquele indice é {id: '1', nome:'Livro UM'} e o objeto que vem de modificacoes é {nome: 'OUTRO TITULO QUALQUER'}.

- Essa linha de código vai comparar ambos os objetos e caso o objeto modificações tiver uma propriedade igual ao objeto livroAtuais[indiceModificado], ele vai fazer essa alteração. E caso o objeto modificacoes tiver uma propriedade nova, ele vai vai adicionar essa propriedade nova no objeto livroAtuais[indiceModificado].

E com isso nosso novo objeto com as modifilçoes ficará salvo na const conteudoMudado que nesse nosso exemplo será {id: '1', nome:'OUTRO TITULO QUALQUER'}.

Seguindo a explicação da função, após ele criar esse objeto novo com as modificações, temos que dizer que o item do index buscado será esse novo objeto, ou seja, vamos escrever por cima o item novo.

E por último escrevemos o código fs.writeFileSync('livros.json', JSON.stringify(livroAtuais)) para subescrever todo o arquivo, mas agora com o array de itens todo atualizado.


Seguimos agora para CONTROLADORES:

    function patchLivro(req, res) {
        try {

            const id = req.params.id
            const body = req.body

            modificaLivro(body , id)

            res.send('Livro modificado com sucesso!')
            
        } catch (error) {
            res.status(500)
            res.send(error.message)
        }
    }

Aqui basicamente seguimos o padrão, mas pegamos agora tanto o id atrvés da rota e também os dados da modificação pelo body, chamamos a função  modificaLivro(body , id) e enviamos uma mensagem de sucesso.

ROTAS:

    router.patch('/:id', patchLivro)

Apenas uma rota padrão, mas com o método patch.