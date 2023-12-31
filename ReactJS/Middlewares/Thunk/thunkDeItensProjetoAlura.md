# Thunk de itens

Apenas criamos a parte do Thunk para buscar os itens também:

Pasta services no arquivo itens.js:

    import instance from "common/config/api"

    const itensService = {
        buscar: async () => {
            const resposta = await instance.get('/itens')

            return resposta.data
        }
    }

    export default itensService

Arquivo itens.js da pasta de reducers:

    extraReducers: builder => {
        builder.addCase(
            buscarItens.fulfilled,
            (state, { payload }) => {
                state.push(...payload)
            }
        )
    }

E na pagina Home:

    useEffect(() => {
        dispatch(buscarCategorias())
        dispatch(buscarItens())
    }, [dispatch])

Dessa forma já conseguimos buscar tanto os itens como as categorias direto da API, mas ainda temos a questão da duplicação de itens que temos que ver.


