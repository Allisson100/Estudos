# createAsyncThunk

Vamos criar esse middleware em nosso reducer de categorias.

Primeiro por questão de estruturação do projeto vamos criar uma pasta dentro de src com o nome services. Tudo que se remete a quisição para uma api fica nessa pasta e como queremos buscar na API os dados de catogorias, então vamos criar um arquivo chamado categorias.js e nele digitamos:

    import instance from "common/config/api"

    const categoriasService = {
        buscar: async () => {
            const resposta = await instance.get('/categorias')

            return resposta.data
        }
    }

    export default categoriasService

Aqui utilizamos nossa instancia do axios atrvés da const instance e apenas fazemos uma requisição normal. E basciamente colocamos essa nossa função dentro de um objeto.

Agora do arquivo categorias.js da pasta reducer colocamos digitamos:

    import { createAsyncThunk, createSlice } from '@reduxjs/toolkit';
    import categoriasService from 'services/categorias';

    const initialState = [];

    export const buscarCategorias = createAsyncThunk(
        'categorias/buscar',
        categoriasService.buscar
    )

    const categoriasSlice = createSlice({
        name: 'categorias',
        initialState,

        reducers: {
            adicionarCategorias: (state, { payload }) => {
                state.push(...payload)
            },
        },

        extraReducers: builder => {
            builder.addCase(
                buscarCategorias.fulfilled,
                (state, { payload }) => {
                    state.push(...payload)
                }
            )
        }
    });

    export const { adicionarCategorias } = categoriasSlice.actions

    export default categoriasSlice.reducer;

Criamos primeiro a const buscarCategorias:

    export const buscarCategorias = createAsyncThunk(
        'categorias/buscar',
        categoriasService.buscar
    )

Aqui é onde utilizamos o createAsyncThunk e nele devemos configurar passando uma string que nesse caos foi 'categorias/buscar', pois esse nome já diz muito bem o que vamos fazer. E como segunda configuração temos que passar a função que vai fazer a request na api, que nesse caso é a função que vem lá da pasta services, categoriasService.buscar.

Como sabemos o middleware cria uma action, então devemos passar essa action para o reducer, mas não da maneira tradicional do redux, pois o middleware é como se fosse um componente extra do redux. Então a forma que adicionamos essa action no reducer é:

    extraReducers: (builder) => {
        builder.addCase(
            buscarCategorias.fulfilled,
            (state, { payload }) => {
                state.push(...payload)
            }
        )
    }

Utilzamos um método chamado extraReducers e nele temos um parâmetro que chamamos de builder e com ele podemos tem acesso a um método chamado addCase() que justamente nos ajudar a adiconar essa aciotn 'extra' que criamos com o thunk.

Depois disso o thunk cria como se fosse três actions por requisição, que é a pending, o fulfilled e o rejected, que basicamente são as fases de uma resolução de promisse. Então pegamos o caso fulfilled, ou seja, deu certo a requisição na API e depois setamos o state normalmente como qualuqer outra action:

    (state, { payload }) => {
        state.push(...payload)
    }

É importante prestar atenção que o extraReducers não fica dentro do objeto reducers.

Agora no nosso componente Home:

    useEffect(() => {
        dispatch(buscarCategorias())
        buscarItens()
    }, [dispatch , buscarItens])

Nós apenas fazemos o disptach na função buscarCategorias que vem lá do reducer categorias.js:

    export const buscarCategorias = createAsyncThunk(
        'categorias/buscar',
        categoriasService.buscar
    )

O único problema agora é que nossa parte de categorias na página inicial está sendo duplicada, vamos resolver isso depois.
