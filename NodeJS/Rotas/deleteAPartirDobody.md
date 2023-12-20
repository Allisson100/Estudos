# Delete a partir do body

Criamos agora a rota de deletar e basicamente a rota retorna o lista de itens, mas apenas com os livros que são diferentes do id que foi passado como parâmetro.

Rota:

    router.delete('/:id', deleteLivro)

Controladores:

    function deleteLivro(req, res) {
        try {

            const id = req.params.id

            deletarLivroPorId(id)

            res.send('Livro deletado com sucesso!')
            
        } catch (error) {
            res.status(500)
            res.send(error.message)
        }
    }

Servicos:

    function deletarLivroPorId (id) {
        const livros = JSON.parse(fs.readFileSync('livros.json'))

        const livrosFiltrados = livros.filter(livro => livro.id !== id)
        
        fs.writeFileSync('livros.json', JSON.stringify(livrosFiltrados))
    }

