# HerancaDeClasse

# Herança de classe

Criamos a herança de classe:

    import User from "./User.js";

    class Admin extends User {
        constructor(nome, email, nascimento, role = 'admin', ativo = true) {
            super(nome, email, nascimento, role, ativo)
        }
    }

    const novoAdmin = new Admin ("Lionel", "l@L", "2021-01-01")
    console.log(novoAdmin);
    console.log(novoAdmin.exibirInfos());

Com a função super() dentro do constructor() podemos definir quais variáveis queremos reutilizar da classe User.

E dessa forma a classe Admin também herda a função exibirInfos() da classe User.
