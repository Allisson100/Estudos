# Erros de validação

No tratamento de erros de nossa aplicação, quando o front end envia um body vazio para cadastrar um autor ou um livro novo por exemplo, a mensagem de erro sempre era erro interno no servidor, mas na verdade isso é um erro de validação lá do formulário do front end.

Então para resolver isso fizemos a seguinte validação em nosso arquivo manipuldaroDeErros.js:

    import mongoose from "mongoose";

    // eslint-disable-next-line no-unused-vars
    function manipuladorDeErros(erro, req, res, next) {
        if(erro instanceof mongoose.Error.CastError) {
            res.status(400).send({message: "Um ou mais dados fornecidos estão incorretos"});
        } else if (erro instanceof mongoose.Error.ValidationError) {

            const mensagensErro = Object.values(erro.errors).map(erro => erro.message).join("; ");

            res.status(400).send({message: `Os seguintes erros foram encontrados: ${mensagensErro}`});
        }else {
            res.status(500).send({message: "Erro interno de servidor."});
        }
    }

    export default manipuladorDeErros;

Criamos a linha:

    const mensagensErro = Object.values(erro.errors).map(erro => erro.message).join("; ");

Nesse caso o Object.values pega os valores das propriedades do objeto erro.errors e depois aplica um map para obeter as mensagens desses erros e essas mensagens como itens no array mensagensErro. Depois disso utilizamos o join apenas para concatenar esses itens do arrays.

Para personalizar essas mensagens tivemos que alterar nossos models tanto de livros como de autores:

Model Autor.js:

    import mongoose from "mongoose";

    const autorSchema = new mongoose.Schema(
        {
            id: {type: String},
            nome: {
                type: String, 
                required: [true, "O nome do(a) autor(a) é obrigatório."]
            },
            nacionalidade: {type: String}
        },
        {
            versionKey: false
        }
    );

    const autores = mongoose.model("autores", autorSchema);

    export default autores;

Model Livro.js:

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
                required: [true, "A editora é obrigatória"]
            },
            numeroPaginas: {type: Number}
        }
    );

    const livros= mongoose.model("livros", livroSchema);

    export default livros;

No campo required podemos utilizar uma forma de per dir que o required seja true e também passar qual mensagem vai ser referente aquele campo caso tenha algum erro nele e para isso utilizamos o [].