# Sintaxe de espalhamento

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

    function ligaParaCliente (telefoneComercial, telefoneResidencial) {
        console.log(`Ligando para ${telefoneComercial}`)
        console.log(`Ligando para ${telefoneResidencial}`)
    }

    ligaParaCliente(cliente.telefone[0], cliente.telefone[1])

Podemos chamar a função dessa forma também:

    ligaParaCliente(...cliente.telefone)

Outro exemplo:

    const encomenda = {
        destinatario: cliente.nome,
        ...cliente.endereco[0],
    }

Dessa forma ele espealha o objeto que está dentro de enderecos, o que facilita se não deveriamos fazer o seguinte:

    const encomenda = {
        destinatario: cliente.nome,
        rua: cliente.endereco[0].rua
        // E assim sucessivamente com todos os campos
    }
