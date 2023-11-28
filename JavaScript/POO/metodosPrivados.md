# MetodosPrivados

# Métodos privados

Podemos também criar métodos privados:

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

        #montaObjUser() {
            return ({
                nome: this.#nome,
                email: this.#email,
                nascimento: this.#nascimento,
                role: this.#role,
                ativo: this.#ativo
            })
        }

        exibirInfos() {
            const objUser = this.#montaObjUser()
            return `${objUser.nome}, ${objUser.email}, ${objUser.nascimento}, ${objUser.role}, ${objUser.ativo}`
        }
    }

Nós temos um método muito importante para o código e por isso colocamos como privado #montaObjUser(), mas podemos fazer o uso de um método público exibirInfos(), para chamar esse método privado e ai sim pegar os dados o "jogá-los" para fora da classe.

No arquivo Admin.js:

    import User from "./User.js";

    export default class Admin extends User {
        constructor(nome, email, nascimento, role = 'admin', ativo = true) {
            super(nome, email, nascimento, role, ativo)
        }

        nomeAdmin() {
            return `${this.nome}`
        }

        criarCurso(nomeDoCurso, vagas) {
            return `Curso de ${nomeDoCurso} criado com ${vagas} vagas`
        }
    }

Criamos um novo método chamado nomeAdmin() em que tentamos retornar uma variável privada da classe User.

Quando rodados isso o terminal nos retorna undefined, pois quela variável está privada em outra classe, vamos tem que aprender como resolver isso.
