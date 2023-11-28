# AtributosPrivados

# Atributos privados

Estamos aprendendo a deixar a nossa classe privada, a seguir vou mostrar uma forma que se pode alterar os dados livremente:

    import User from "./User.js";
    import Docente from "./Docente.js";
    import Admin from "./Admin.js";

    const novoUser = new User ('Allisson', 'a@a.com', '2021-01-01')

    console.log(novoUser.exibirInfos());

    novoUser.nome = 'teste'
    console.log(novoUser.nome);
    console.log(novoUser.exibirInfos());

E a gente nãoq uer qu isso aconteça, não queremos poder mudar o nome do usuário por exemplo em qualquer momento.

Para resolver fazemos o seguinte, na nossa classe User adicionamos a #:

    export default class User {
        #nome
        #email
        #nascimento
        #role
        #ativo

        constructor(nome, email, nascimento, role, ativo = true) {
            this.#nome = nome
            this.#email = email
            this.#nascimento = nascimento
            this.#role = role || 'estudante'
            this.#ativo = ativo
        }

        exibirInfos() {
            return `${this.#nome}, ${this.#email}`
        }
    }

E temos que lembrar de adicionar as variaveis com # antes do constructor.
