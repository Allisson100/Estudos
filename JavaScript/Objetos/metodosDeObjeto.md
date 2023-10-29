# Métodos de objeto

    const cliente = {
        nome: "João",
        idade: 24,
        email: "joao@frim.com",
        telefone: ["1156565656", "116565656"],
    }

    cliente.endereco = {
        rua: "qualquer endreço aqui",
        numero: 1124,
        apartamento: true,
        complemento: "ap 934",
    }

    const chavesDoObjeto = Object.keys(cliente)
    console.log(chavesDoObjeto) // ['nome', 'idade', 'email', 'telefone', 'endereco']
