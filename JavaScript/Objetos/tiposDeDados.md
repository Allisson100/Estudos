# Tipos de dados e valores

    const cliente = {
        nome: "João",
        idade: 24,
        email: "joao@frim.com",
        telefone: ["1156565656", "116565656"],
    }

# Objetos em objetos

    const cliente = {
        nome: "João",
        idade: 24,
        email: "joao@frim.com",
        telefone: ["1156565656", "116565656"],
    }

    cliente.endereco = {
        rua: "qualuqer endreço aqui",
        numero: 1124,
        apartamento: true,
        complemento: "ap 934",
    }

# Listas de objetos

    cliente.enderecos = [
        {
            rua: "qualuqer endreço aqui",
            numero: 1124,
            apartamento: true,
            complemento: "ap 934",
        },
    ]

    clientes.ederecos.push({
        rua: "qualquer endreço aqui",
        numero: 5897,
        apartamento: false,
    })

    const listaApenasApartamento = cliente.enderecos.filter(
        (endereco) => endereco.apartamento === true
    )

# Funções

    const cliente = {
        nome: "João",
        idade: 24,
        email: "joao@frim.com",
        telefone: ["1156565656", "116565656"],
        saldo: 200,
        efetuaPagamento: function (valor) {
            if(valor > this.saldo) {
                console.log("Saldo insuficiente")
            } else {
                this.saldo -= valor
                console.log(`Pagamento realizado, novo saldo é: ${this.saldo}`)
            }
        }
    }

    cliente.efetuaPagamento(250)
