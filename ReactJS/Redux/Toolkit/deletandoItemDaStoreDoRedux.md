# Deletando item

Criamos a action de deletar de acordo com o que a documentação do Immer sugere:

    deletarItem: (state, { payload }) => {
        const index = state.findIndex(item => item.id === payload)
        state.splice(index, 1)
        console.log(payload);
    }

Lembrando que podemos utilzar .map() e .filter() utilizando o return junto, mas vale lembrar que o Immer não recomenda fazer dessa forma, então por isso é sempre ideal fazer da forma como a documentação pede.