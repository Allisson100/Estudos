# Aplicando o Toast

Apenas para demonstração de como o Toast funciona, acrescentamos ele no nosso reducer de categorias:

    const { toast } = createStandaloneToast()

    extraReducers: builder => {
        builder
        .addCase(
            buscarCategorias.fulfilled,
            (state, { payload }) => {
                toast({
                    title: 'Sucesso!',
                    description: 'Categorias carregadas com sucesso',
                    status: 'success',
                    duration: 2000,
                    isClosable: true
                })
                return payload
            }
        )
        .addCase(
            buscarCategorias.pending,
            (state, { payload }) => {
                toast({
                    title: 'Carregando!',
                    description: 'Carregando categorias',
                    status: 'loading',
                    duration: 2000,
                    isClosable: true
                })
            }
        )
        .addCase(
            buscarCategorias.rejected,
            (state, { payload }) => {
                toast({
                    title: 'Erro!',
                    description: 'Erro na busca de categorias',
                    status: 'error',
                    duration: 2000,
                    isClosable: true
                })
            }
        )
    }