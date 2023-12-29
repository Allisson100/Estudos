# Criando autores

Criamos o model de Autor:

    import mongoose from "mongoose"

    const autorSchema = new mongoose.Schema({
        id: { type: mongoose.Schema.Types.ObjectId },
        nome: { types: String, required: true },
        nacionalidade: { type: String }
    }, { versionKey: false })

    const autor = mongoose.model('autores', autorSchema)

    export { autor , autorSchema }