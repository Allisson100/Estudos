# Validações do Mongoose

Criamos validações atrvés do mongoose. Em no arquivo Livro.js digitamos:

    import mongoose from "mongoose";

    const livroSchema = new mongoose.Schema(
        {
            id: {type: String},
            titulo: {
                type: String, 
                required: [true, "O título do livro é obrigatório"]
            },
            autor: {
                type: mongoose.Schema.Types.ObjectId, 
                ref: "autores", 
                required: [true, "O autor é obrigatório"]
            },
            editora: {
                type: String, 
                required: [true, "A editora é obrigatória"],
                enum: {
                    values: ["Casa do código", "Alura"],
                    message: "A editora {VALUE} não é um valor permitido"
                }
            },
            numeroPaginas: {
                type: Number,
                min: [10, "O número de páginas deve estar entre 10 e 5000. Valor fornecido: {VALUE}"],
                max: [5000, "O número de páginas deve estar entre 10 e 5000. Valor fornecido: {VALUE}"]
            }
        }
    );

    const livros= mongoose.model("livros", livroSchema);

    export default livros;

Como podemos ver o próprio mongoose no da a possibilidade de validar alguns dados. No número de páginas definimos um valor máximo e mínimo e colocamos as mensagens para casa aconteça esse erro.

Utilizamos também uma validação para a string, no caso o campo editora. Com a propriedade enum, podemos passar um objeto e dentro dele passamos um array com os valores que vamos aceitar para editora, nesse caso apenas valores como 'Cassa do código' e 'Alura' serão aceitos, caso colocarem outro valor um erro será enviado e o erro está na propriedade message.

Lembrando que também utilizamos o {VALUE}, pois dessa forma podemos informar ao usuário qual valor ele forneceu e tem que ser escrito exatemente dessa forma, {VALUE}.