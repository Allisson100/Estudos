# OOComJavaScript

# OO com JavaScript

Criamos um arquivo js chamado objetoLiteral.js e nele digitamos:

    const user = {
        nome: 'Juliana',
        email: 'j@j.com',
        nascimento: '2021/01/01',
        role: 'admin',
        ativo: true,
        exibirInfos: function() {
            console.log(this.nome, this.email)
        }
    }

# Entendendo o this

    const user = {
        nome: 'Juliana',
        email: 'j@j.com',
        nascimento: '2021/01/01',
        role: 'admin',
        ativo: true,
        exibirInfos: function() {
            console.log(this.nome, this.email)
        }
    }

    user.exibirInfos() //Juliana j@j.com
    // const exibir = user.exibirInfos
    // exibir()

    const exibir = function () {
        console.log(this.nome);
    }

    const exibirNome = exibir.bind(user)
    exibirNome() //Juliana
    exibir() //undefined

Como podemos ver o this só funciona com contexto e fizemos um exemplo onde criamos uma função que utiliza o objeto user como referencia através da bind. Então trouxemos contexto para a função exibir pela bind e por isso o this.nome funciona.
