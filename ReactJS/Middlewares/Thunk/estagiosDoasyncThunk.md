# Estágios do async thunk

Criamos os outros estágios do Thunk nos reducer de categorias e dos itens;

categorias.js:

    extraReducers: builder => {
        builder
        .addCase(
            buscarCategorias.fulfilled,
            (state, { payload }) => {
                return payload
            }
        )
        .addCase(
            buscarCategorias.pending,
            (state, { payload }) => {
                console.log('Carregando categorias');
            }
        )
        .addCase(
            buscarCategorias.rejected,
            (state, { payload }) => {
                console.log('Bucas de categoiras rejeitada!');
            }
        )
    }

itens.js:

    extraReducers: builder => {
        builder
        .addCase(
            buscarItens.fulfilled,
            (state, { payload }) => {
                return payload
            }
        )
        .addCase(
            buscarItens.pending,
            (state, { payload }) => {
                console.log('Carregando categorias');
            }
        )
        .addCase(
            buscarItens.rejected,
            (state, { payload }) => {
                console.log('Bucas de categoiras rejeitada!');
            }
        )
    }

Por enquanto colocamos somente um console.log neles, mas já temos os casos de requisição pending, fulfilled e rejected.