# for...in

Com esse metodo no for pordemos fazer um forEach porém em um objeto:

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

    for (let campo in cliente) {
        console.log(campo) // Retorna os nomes de cada propriedade
    }

    for (let campo in cliente) {
        console.log(cliente[campo]) // Retorna os valores de cada propriedade
    }
