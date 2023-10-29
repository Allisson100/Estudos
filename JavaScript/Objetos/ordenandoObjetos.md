# Ordenando objetos

Vamos criar uma função para conseguirmos ordenar os itens da lista de acordo com a propriedade que queremos.

    const clientes = require("./jsonEstudos.json")

    funtion ordenar (lista, propriedade) {
        const resultado = lista.sort((a,b) => {

            if(a[propriedade] < b[propriedade]) {
                return -1
            }

            if(a[propriedade] > b[propriedade]) {
                return 1
            }

            return 0
        })

        return resultado
    }

Se por acaso quisermos colocar a ordenação de forma inversa podemos utilizar:

    resultado.reverse()
