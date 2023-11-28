# Object.create() vs new

# Object.create() vs new

O new serve para criar instancias de objetos através de funções construtoras. Vamos criar um arquivo novo chamado new.js e nele digitamos:

    function User (nome, email) {
        this.nome = nome
        this.email = email

        this.exibirInfos = function() {
            return `${this.nome}, ${this.email}`
        }
    }

    const novoUser = new User('Allisson', 'a@a.com')
    console.log(novoUser.exibirInfos());

Devemos usar letra maiúscula quando estamos trabalhando com esse conceito de classes.

O código acima é a forma de criarmos objetos com Javascript utilizando um construtor.

    function User (nome, email) {
        this.nome = nome
        this.email = email

        this.exibirInfos = function() {
            return `${this.nome}, ${this.email}`
        }
    }

    // const novoUser = new User('Allisson', 'a@a.com')
    // console.log(novoUser.exibirInfos()); //Allisson, a@a.com

    function Admin(role)  {
        User.call(this, 'Juliana', 'j@j.com')
        this.role = role || 'estudante'
    }

    Admin.prototype = Object.create(User.prototype)

    const novoUser = new Admin('admin')
    console.log(novoUser.exibirInfos()); // Juliana, j@j.com
    console.log(novoUser.role); // admin

Nesse código agora estamos referenciando as propriedades e métodos de User para o Admin e estamos criando outro novoUser para teste.

    Admin.prototype = Object.create(User.prototype)

Basicamente passamos para dentro da propriedade prototype de Admin as propriedades de User, então estamos criando um objeto com Objetc.create e passando como parâmetro a propriedade User.prototype, ou seja, os protótipos de User estão sendo passados como base para dentro de Admin.

    const user = {
        exibirInfos: function(nome) {
            return nome
        }
    }

    const novoUser = Object.create(user)

    console.log(novoUser.exibirInfos('Allisson')); //Allisson
    console.log(user.isPrototypeOf(novoUser)); //true

Fizemos esse novo exemplo onde passamos as propriedaes para a const novoUSer através do objeto user. Não estamos usando uma função construtora estamos usando objetos diretamente.

E no caso de:

    console.log(user.isPrototypeOf(novoUser)); //true

Tem que nos retornar true, pois user é um prototype de novoUSer.

    const user = {

        init: function(nome, email) {
            this.nome = nome
            this.email = email
        },

        exibirInfos: function() {
            return this.nome
        }
    }

    const novoUser = Object.create(user)
    novoUser.init('Allisson', 'a@a.com')

    console.log(novoUser.exibirInfos()); //Allisson

E temos esse outro modo de fazer utilizando um construtor que nesse caso é o init.
