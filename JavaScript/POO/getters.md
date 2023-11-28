# Getters

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
    }

Utilizamos o get para meio que dar permissão para o código utilizar algumas variáveis privadas. Vale lembrar que o get não recebe parâmetro e faz perte de uma metodologia criar um get para cada prorpriedade que queremos deixa disponível.

E para utiliza-lo em outro arquivo digitamos:

    const novoAdmin = new Admin ('CR7', 'c@c.com', '2021-01-01')
    console.log(novoAdmin.nascimento);

Não precisamos chamar como uma função, exemplo nascimento(), como utilizamos o get chamamos as propriedades como se fosse propriedades mesmo.

Vale lembrar também que nçao conseguimo alterar as propriedades, o get deixa você ver a propriedade em outra parte do código, mas somente como mode de leitura.
