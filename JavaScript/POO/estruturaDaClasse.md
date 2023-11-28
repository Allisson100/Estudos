# 1. EstruturaDaClasse

# Estrutura da classe

Criamos uma classe pela primeira vez:

    class User {
        constructor(nome, email, nascimento, role, ativo = true) {
            this.nome = nome
            this.email = email
            this.nascimento = nascimento
            this.role = role || 'estudante'
            this.ativo = ativo
        }

        exibirInfos() {
            return `${this.nome}, ${this.email}`
        }
    }

    const novoUser = new User('Allisson', 'a@a.com', '2000-11-16')
    console.log(novoUser);
    console.log(novoUser.exibirInfos());
