# Buscando categorias

Vamos começar instalando o axios:

    yarn add axios

Agora camos criar uma pasta dentro de src com o nome common, dentro dela outra pastat chamada config e dentro de config vamos criar um arquivo chamamdo api.js e nele digitamos:

    import axios from 'axios'

    const instance = axios.create({
        baseURL: 'http://localhost:3001'
    }) 

    export default instance

Criamos uma instancia do axios com a url base do nosso servidor.

Agora no nosso componente da pagina HOME utilizamos um useEffect:

    const buscarCategorias = useCallback(async () => {
        const resposta = await instance.get('/categorias')

        dispatch(adicionarCategorias(resposta.data))
    }, [dispatch])

    useEffect(() => {
        buscarCategorias()
    }, [buscarCategorias])

E também modificamos o reducer categorias.js:

    import { createSlice } from '@reduxjs/toolkit';

    const initialState = [];

    const categoriasSlice = createSlice({
        name: 'categorias',
        initialState,

        reducers: {
                adicionarCategorias: (state, { payload }) => {
                state.push(...payload)
            }
        }
    });

    export const { adicionarCategorias } = categoriasSlice.actions

    export default categoriasSlice.reducer;

E como vimos criamos uma aciton na categorias para conseguirmos atualizar o estado das categorias atrvés do nosso servidor.

A nossa função buscarCategorias utiliza o useCallback, pois como é uma função que está buscando dados do servidor, não queremos que toda vez que o compoennte seja redenrizado a função busque de novo os itens na api, ou seja, temos que utilizar o useCallback, pois ele fará isso apenas uma vez.

E depois que fizemos a requisição podemos salvar os dados na store de categorias através do disptach().

Ainda não utilizamos oThunk, mas vamos melhorando.