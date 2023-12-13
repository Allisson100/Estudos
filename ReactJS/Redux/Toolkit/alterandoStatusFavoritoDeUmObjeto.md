# Mudando maps e favoritos

Nós apenas mudamos a parte da action:

    const itensSlice = createSlice({
        name: 'itens',
        initialState,
        reducers: {
            mudarFavorito: (state, { payload }) => {
                state = state.map(item => {
                    if(item.id === payload) item.favorito = !item.favorito

                    return item
                })
            }
        }
    })

Agora de vez escrever no cosole, nós mudamos para que através do map o item que tiver o mesmo item do payload, deverá ter seu favorito inverso, ou seja, true vira false e false vira true.