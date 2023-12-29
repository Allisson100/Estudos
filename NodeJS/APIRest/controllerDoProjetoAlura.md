# Controller DELETE

Organizamos melhor o projeto, criamos um pasta chamada routes e dentro dela dois arquivos um chamado index.js que será onde ficará todas as rotas e criamos assim já pensando que no futuro possa ter diversas rotas para diversas collections diferentes e também outro arquivo chamado livrosRoutes.js que é para as rotas da coleection livros.

Arquivo livrosRoutes.js:

    import express from 'express'
    import LivroController from '../controllers/livroController.js'

    const routes = express.Router()

    routes.get('/livros', LivroController.listarLivros)
    routes.get('/livros/:id', LivroController.listarLivroPorId)
    routes.post('/livros', LivroController.cadastrarLivro)
    routes.put('/livros/:id', LivroController.atualizarLivro)
    routes.delete('/livros/:id', LivroController.excluirLivro)

    export default routes

Arquivo index.js:

    import express from "express"
    import livros from './livrosRoutes.js'

    const routes = (app) => {
        app.route('/').get((req, res) => res.status(200).send('Curso de Node.js'))
        app.use(express.json(), livros)
    }

    export default routes

E no nosso arquivo app.js ficou assim:

    import express from 'express'
    import conectaNaDatabase from './config/dbConnect.js'
    import routes from './routes/index.js'

    const conexao = await conectaNaDatabase()

    conexao.on('error', (erro) => {
        console.error('Erro de conexão', erro)
    })

    conexao.once('open', () => {
        console.log('Conexão com o banco feita com sucesso!');
    })

    const app = express()
    routes(app)

    export default app

Como podemos ver tem a parte da conexão ao Mongo e depois temos a const app e a função routes(app) que recebe commo parâmetro o próprio app.

Esse routes nada mais é que a função que criamos no arquivo index.js, como eu disse esse arquivo vai direcionar para todas as rotas existentes por questões de organização.

Como podemos ver no arquivo livroRoutes.js utilizamos controllers, então criamos uma pasta dentro de src chamada controllers e dentro dela temos um arquivo chamado livroController.js:

    import livro from "../models/Livro.js"

    class LivroController {

        static async listarLivros (req, res) {
            try {
                const listaLivros = await livro.find({})
                res.status(200).json(listaLivros)

            } catch (erro) {
                res.status(500).json({
                    message: `${erro.message} - Falha ao cadastrar livro`
                })
            }
        }

        static async listarLivroPorId (req, res) {
            try {
                const id = req.params.id
                const livroEncontrado = await livro.findById(id)
                res.status(200).json(livroEncontrado)

            } catch (erro) {
                res.status(500).json({
                    message: `${erro.message} - Falha na requisição do livro`
                })
            }
        }

        static async atualizarLivro (req, res) {
            try {
                const id = req.params.id
                const body = req.body

                await livro.findByIdAndUpdate(id, body)
                res.status(200).json({
                    message: 'Livro atualizado'
                })

            } catch (erro) {
                res.status(500).json({
                    message: `${erro.message} - Falha na atualização do livro`
                })
            }
        }

        static async cadastrarLivro (req, res) {
            try {
                const novoLivro = await livro.create(req.body)
                res.status(201).json({
                    message: 'Criado com sucesso',
                    livro: novoLivro
                })

            } catch (erro) {
                res.status(500).json({
                    message: `${erro.message} - Falha ao cadastrar livro`
                })
            }
        }

        static async excluirLivro (req, res) {
            try {
                const id = req.params.id

                await livro.findByIdAndDelete(id)
                res.status(200).json({
                    message: 'Livro deletado com sucesso'
                })

            } catch (erro) {
                res.status(500).json({
                    message: `${erro.message} - Falha na exclusão do livro`
                })
            }
        }
    }

    export default LivroController

Nesse arquivo através de uma classe e de métodos desenvolvemos toda a lógica que estaria presente nas rotas deixando o código mais organizado.

Também utilizamos funções do prórpio mongoose para nos ajudar a utilizar os métodos como GET,POST,PUT e DELETE no banco de dados.

Acrescentamos o try catch, para nos auxiliar tanto no sucesso quanto na falhar ao tentar fazer alguma operações no banco de dados e também na parte de response, colocamos json mais personalizados com um obejto contendo alguns dados.

Todos esse métodos do mongoose está na documentação dele e lá ele explica também como se utiliza e como se deve passar os parâmetros.