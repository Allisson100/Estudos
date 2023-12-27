# Finalizando edição

Temos algumas formas de mudar o state da store itens para que modificar o tpitulo do item.

Primeiro:

O return no Immer significa que estamos retornando um estado completamente novo.

    mudarItem: (state , { payload }) => {
        return state.map(item => {
            if (item.id === payload.id) item = {...item, ...payload.item}
            return item
        })
    }

Dessa maneira temos que colocar o return, pois no Immer isso indica que criamos um estado totalmente novo, mesmo que a gente queira mudar somente uma propriedade do objeto nesse caso devemos retornar um objeto totalmente novo por conta da forma como os objetos funcionam no JavaScript.

Porém tem uma forma muito melhor de fazer isso utilizando o Object.assign:

    mudarItem: (state , { payload }) => {
        const index = state.findIndex(item => item.id === payload.id)
        Object.assign(state[index], payload.item)
    }

Dessa forma é o mais recomendado. Primeiro achamos o valor do index do objeto que está dentro do array que queremos modificar. Com o index utilizamos somente o Object.assign(state[index], payload.item) e dizemos que, dentro do state[index], ou seja, no index daquele array, queremos mudar os valores de acordo com o que vem do payload.item, que no nosso caso é somente o título.
