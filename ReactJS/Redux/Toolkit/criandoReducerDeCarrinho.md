# Aplicando o Reducer

Criamos uma novo reducer chamado carrinho.js e nele digitamos:

    import { createSlice } from '@reduxjs/toolkit'

    const initialState = []

    const carrinhoSlice = createSlice({
        name: 'carrinho',
        initialState,
        reducers: {
            mudarCarrinho: (state, { payload }) => {
                const temItem = state.some(item => item.id === payload)
                if(!temItem) return state.push({
                    id: payload,
                    quantidade: 1
                })

                return state.filter(item => item.id !== payload)
            }
        }
    })

    export const { mudarCarrinho } = carrinhoSlice.actions

    export default carrinhoSlice.reducer

Agora vamos no componente Item e adicionar:

    <FaCartPlus 
        {...iconeProps}
        color={true ? '#1875E8' : iconeProps.color}
        className={styles['item-acao']}
        onClick={resolverCarrinho}
    />

    function resolverCarrinho() {
        dispatch(mudarCarrinho(id))
    }

Criamos um onClick no icone de carrinho do produto e também criamos uma função para fazer o dispatch da action, porém isso dá um erro de imutabilidade,

O erro ocorre, pois estamos alterando o estado do carrinho, uma hora estamos adicionando o item e outra hora estamos removendo esse item e dessa forma estamos alterando o state drasticamente vamos dizer assim.

Isso é diferente com o que ocorre no caso da alteração de estado da action que existe no reducer dos itens, pois estamos apenas mudando o status de favorito de um iterm que já existe dentro do estado.

Então precisamos arrumar isso na parte do carrinho.

Então na action do carrinho mudamos:

    import { createSlice } from '@reduxjs/toolkit'

    const initialState = []

    const carrinhoSlice = createSlice({
        name: 'carrinho',
        initialState,
        reducers: {
            mudarCarrinho: (state, { payload }) => {
                const temItem = state.some(item => item.id === payload)

                if(!temItem) return [
                    ...state,
                    {
                        id: payload,
                        quantidade: 1
                    }
                ]

                return state.filter(item => item.id !== payload)
            }
        }
    })

    export const { mudarCarrinho } = carrinhoSlice.actions

    export default carrinhoSlice.reducer

Pois dessa forma:

    const temItem = state.some(item => item.id === payload)

    if(!temItem) return [
        ...state,
        {
            id: payload,
            quantidade: 1
        }
    ]

Estamos adicionando adicionando um novo estado e não mudando o estado atualk com o método push.