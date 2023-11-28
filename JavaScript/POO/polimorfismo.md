# Polimorfismo

no caso os métodos tem que ter o mesmo nome e os mesmo parâmetro caso precisem, mas os métodos podem presentar comportamentos diferentes dependendo da subclasse.

Exemplo:

Arquivo User.js:

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

        get nome() {
            return this.#nome
        }

        get email() {
            return this.#email
        }

        get nascimento() {
            return this.#nascimento
        }

        get role() {
            return this.#role
        }

        get ativo() {
            return this.#ativo
        }

        set nome (novoNome) {
            if(novoNome == '') {
                throw new Error('formato inválido')
            }
            this.#nome = novoNome
        }

        exibirInfos() {
            return `${this.nome}, ${this.email}, ${this.nascimento}, ${this.role}, ${this.ativo}`
        }
    }

Arquivo Admin.js:

    import User from "./User.js";

    export default class Admin extends User {
        constructor(nome, email, nascimento, role = 'admin', ativo = true) {
            super(nome, email, nascimento, role, ativo)
        }

        exibirInfos() {
            return `${this.nome}, ${this.ativo}`
        }

        criarCurso(nomeDoCurso, vagas) {
            return `Curso de ${nomeDoCurso} criado com ${vagas} vagas`
        }
    }

Podemos ver que o método exibirInfos() tem a mesma assinatura, mas faz coisas diferentes.
