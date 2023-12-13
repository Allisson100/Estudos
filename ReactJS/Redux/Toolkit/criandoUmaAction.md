# Criando uma Action #1

Agora que queremos mudar o farorito dos itens e precisamos criar uma action para isso, então no arquivo itens.js da pasta reducers digitamos:

    const itensSlice = createSlice({
        name: 'itens',
        initialState,
        reducers: {
            mudarFavorito: (state, params) => {
                console.log('state: ', state);
                console.log('paarams: ', params);
            }
        }
    })

    export const { mudarFavorito } = itensSlice.actions

    export default itensSlice.reducer

Agora adicionamos no arquivo a parte de reducers.

Em nosso componente Item, precisamos utilizar essa action:

    {favorito 
        ? <AiFillHeart {...iconeProps} color='#ff0000' className={styles['item-acao']} onClick={resolverFavorito} /> 
        : <AiOutlineHeart {...iconeProps} className={styles['item-acao']} onClick={resolverFavorito} />
    }

Nessa parte do componente que são os icones de coração para favoritar ou não criamos um onClick para chamar a função resolverFavorito:

    import { useDispatch } from 'react-redux'
    import { mudarFavorito } from 'reducers/itens'

    const dispatch = useDispatch()

    function resolverFavorito() {
        dispatch(mudarFavorito(id))
    }

Então primeiro criamos primeiro o dispatch com o hook useDisptach e depois importamos nossa action e utilizamos o dispatch nela, dessa forma quando clicamos no coração, no console já aparece o payload que no nosso caso é o id e o type da action. Agora precisamos mudar o estado de favorito do componente.

