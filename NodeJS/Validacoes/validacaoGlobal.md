# Validação global

Criamos uam validação global para os campos do tipo string com o mongoose. Para fazer isso precisamos fazer a validação antes da importação dos modelos, então para isso criamos um arquivo index.js dentro da pasta models:

    import "./validadorGlobal.js";
    import autores from "./Autor.js";
    import livros from "./Livro.js";

    export {
        autores,
        livros
    };

Como podemos ver primeiro importamos nossa validação e depois os dois modelos e exportamos eles como objeto. Vale lembrar que me nossos arquivos de Controllers onde utilizamos os models devemos arrumar as importações, pois agora ele vem do arquivo index.js.

Em nosso arquivo valiadadorGlobal.js que também está em nossa pasta models digitamos:

    import mongoose from "mongoose";

    mongoose.Schema.Types.String.set("validate", {
        validator: (valor) => valor !== "",
        message: ({ path }) => `O campo ${path} foi fornecido em branco`
    });

Dessa forma conseguimos validar todos os campos do tipo string que não tem como propriedade o required. Vale ressaltar aqui que se um campo não é obrogatório (required) não faz muito sentido não aceitar ele em branco, mas como estamos apenas estudando utilizamos esse recurso para aprender.