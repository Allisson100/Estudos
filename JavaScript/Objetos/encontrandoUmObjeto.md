# Encontrando um objeto

    const clientes = require("./jsonEstudos.json")

    function encontrar (lista, chave, valor) {
        return lista.find((item) => item[chave] === valor)
    }

    const encontrado = encontrar(clientes, "nome", "Kirby")

Se a gente tentar obter os dados de alguem passando como parametro o telefone e o numero desse telefone, a função não vai achar ninguem, pois como usamos comparação estrita, uma string é diferente de um array que contém duas strings, então para melhorar nosso código vamos fazer:

    function encontrar (lista, chave, valor) {
        return lista.find((item) => item[chave].includes(valor))
    }

# Filtrando objetos

Pode acontecer de ter usuarios que moram em apartamento e não colocaram o complemento, então para isso vaom criar uma função para filtrar esses usuarios, para posteriormente avisá-los para arrumarem o cadastro.

    const clientes = require("./jsonEstudos.json")

    function filtrarApartamentosSemComplemento (clientes) {
        return clientes.filter((cliente) => {
            return (cliente.endereco.apartamento && !cliente.endereco.hasOwnProperty("complemento"))
        })
    }

    const filtrados = filtrarApartamentosSemComplemento(clientes)
