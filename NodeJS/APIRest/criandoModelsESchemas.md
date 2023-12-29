# Criando models e schemas

- Schema é um objeto de configuração que define a estrutura e as propriedades de um documento.
- Modelo é um objeto que representa uma coleção na base de dados.

Criamos uma pasta na raiz do projeto que se chama models e dentro dela criamos um arquivo chamado Livro.js:

    import mongoose from "mongoose"

    const livroSchema = new mongoose.Schema({
        id: { type: mongoose.Schema.Types.ObjectId },
        titulo: { type: mongoose.Schema.Types.String, required: true },
        editora: { type: mongoose.Schema.Types.String },
        preco: {type: mongoose.Schema.Types.Number},
        peginas: {type: mongoose.Schema.Types.Number}
    })

Podemos escreve da forma simplificada também:

    import mongoose from "mongoose"

    const livroSchema = new mongoose.Schema({
        id: { type: mongoose.Schema.Types.ObjectId },
        titulo: { type: String, required: true },
        editora: { type: String },
        preco: {type: Number},
        peginas: {type: Number}
    })

Isso é basicamente uma configuração de quais informações e os tipos dessaa informações um livro irá ter.

E por fim:

    import mongoose from "mongoose"

    const livroSchema = new mongoose.Schema({
        id: { type: mongoose.Schema.Types.ObjectId },
        titulo: { type: String, required: true },
        editora: { type: String },
        preco: {type: Number},
        peginas: {type: Number},
    }, { versionKey: false })

    const livro = mongoose.model('livros', livroSchema)

    export default livro

Na const livros colocamos entre aspas o nome da nossa collection lá do banco de dados e depois exportamos essa const para podermos usar no restante do nosso projeto.