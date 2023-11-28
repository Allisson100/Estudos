# Setters

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
            this.#nome = novoNome
        }
    }

Utilizamos o:

    set nome (novoNome) {
        this.#nome = novoNome
    }

Dessa forma conseguimos modificar o valor da propriedade,e para fazer isso:

    const novoAdmin = new Admin ('CR7', 'c@c.com', '2021-01-01')
    console.log(novoAdmin.nome);
    novoAdmin.nome = 'Messi'
    console.log(novoAdmin.nome);

Criamos um novo admin com o nome CR7, mas depois mudamos para Messi.

Vale lembra que o set recebe apenas um parâmetro que é o novo nome que a propriedade vai ter.

Tanto no setter como no getter podemos criar lógica se precisar, por exemplo:

    set nome (novoNome) {
        if(novoNome == '') {
            throw new Error('formato inválido')
        }
        this.#nome = novoNome
    }

Dessa forma caso alguém tentar trocar o nome por uma string vazia, simplesmente teremos um erro.
