# Acessando dados

Mostrou como acessá-lo com o ponto(.).

    const cliente = {
        nome: "Andre",
        idade: 33,
        cpf: "00124541",
        email: "nome@dominio.com",
    }

    console.log(`Os três primeiros número do cpf é ${cliente.cpf.substring(0,3)}`)

# Acessando dados com colchetes

Podemos acessar os itens do objeto da seguinte forma também:

    const cliente = {
        nome: "Andre",
        idade: 33,
        cpf: "00124541",
        email: "nome@dominio.com",
    }

    console.log(`Os três primeiros número do cpf é ${cliente["nome"]}`)
