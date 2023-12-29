# Acessando a coleção livros

Agora estamos refatorando o código para conseguirmos buscar os livros diretamente do MongoDb.

Primeiro apagamos o array de livros que estava ali só de exemplo.

Depois no arquivo app.js digitamos:

    import livro from './models/Livro.js'

    app.get('/livros', async (req,res) => {
        const listaLivros = await livro.find({})
        res.status(200).json(listaLivros)
    })

Primeiro mudamos a rota '/livros', deixamos ela de forma assincrona e salvamos o conteudo do banco de dados na const listaLivros, lembrando que esse método find() é do mongoose que vai se conectar ao MongoDB e vai dar um find e como passamos como parâmetro um arrya vazio ele vai salvar na const todas as ocorrencias que estiver na collection livros, ou seja, irá retornar todos os livros dessa collection.

### dotenv

Instalamos o dotenv apenas para melhorar a parte de conexão naquela url do Mongo Db, pois nossa senha está lá e não queremos que isso suba para o github depois.

    npm i dotenv

Colocamos toda nossa string no arquivo .env e agora nosso arquivo dbConnect.js ficou assim:

    import mongoose from "mongoose";

    async function conectaNaDatabase() {
        mongoose.connect(process.env.DB_CONNECTION_STRING)

        return mongoose.connection
    }

    export default conectaNaDatabase

