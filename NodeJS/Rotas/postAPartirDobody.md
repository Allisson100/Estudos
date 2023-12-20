# Post a partir do body

Agora criamos uam maneira de adicionar um novo item em nosso banco de dados. E vamos fazer isso atrvés do body, claro que isso no front end fica em um formulário, o usuário preenche o formulário e anvia esses dados através do método POST.

Primeiro fizemos uma modificação noa rquivo app.js:

    const express = require('express')
    const rotaLivro = require('./rotas/livros')

    const app = express()
    app.use(express.json())

    app.use('/livros', rotaLivro )


    const port = 8000

    app.listen(port, () => {
        console.log(`App running, port: ${port}`);
    })

Adicionamos a linha app.use(express.json()), pois dessa forma ele nos possibilita a enviar dados com a forma JSON.

Depois como é o padrão criamos a rota e as funções na pasta servicos e controladores.

Rota:

    router.post('/', postLivro)

Lembrando que como queremos adicionar um item utilizamos o método post.

Controlador:

    function postLivro (req, res) {
        try {

            const livroNovo = req.body
            insereLivro(livroNovo)
            res.status(201)
            res.send('Livro inserido com sucesso!')
            
        } catch (error) {
            res.status(500)
            res.send(error.message)
        }
    }

Aqui nós pegamos os dados do novo livro através do req.body e salvamos ele na const livroNovo.

Depois adiconamos ele na função do servico e respondemos tanto com um status 201 como com uma mensagem dizendo se deu certo a inserção do livro no banco de dados.

E por ultimo, Servico:

    function insereLivro(livroNovo) {
        const livros = JSON.parse(fs.readFileSync('livros.json'))

        const novaListaDeLivros = [ ...livros, livroNovo ]

        fs.writeFileSync('livros.json', JSON.stringify(novaListaDeLivros))
    }