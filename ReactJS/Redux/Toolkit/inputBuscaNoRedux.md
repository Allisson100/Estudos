# Finalizando funcionalidades

Adicionamos a funcionalidade da busca para funcionar tanto no carrinho quanto na pagina inicial.

O nosso Componente busca ficou dessa forma:

    import { mudarBusca, resetarBusca } from 'store/reducers/busca';
    import styles from './Busca.module.scss';

    import { useSelector , useDispatch } from 'react-redux';
    import { useEffect } from 'react';
    import { useLocation } from 'react-router-dom';

    export default function Busca() {

        const dispatch = useDispatch()

        const busca = useSelector(state => state.busca)

        const location = useLocation()

        useEffect(() => {

            dispatch(resetarBusca())
            
        }, [location.pathname , dispatch])

        return (
            <div className={styles.busca}>
            <input
                className={styles.input}
                placeholder="O que você procura?"
                value={busca}
                onChange={evento => dispatch(mudarBusca(evento.target.value))}
            />
            </div>
        )
    }

Criamos também o reducer de Busca:

    import { createSlice } from '@reduxjs/toolkit'

    const initialState = ''

    const buscaSlice = createSlice({
        name: 'busca',
        initialState,
        reducers: {
            mudarBusca: (state , {payload}) => payload,
            resetarBusca: () => initialState,
        }
    })

    export const { mudarBusca , resetarBusca } = buscaSlice.actions

    export default buscaSlice.reducer

O estado inicial dele é vazio e ele tem duas actions. Uma delas é só para resetar, pois vamos usar o inout de busca em mais de uma página diferente. E o outro é justamente para controlarmos o estado do input.

Vale lembrar que utilizamos o redux para controlar esse estado, pois vamos usar o  mesmo input em páginas diferentes.

Então no componente de Busca em si, buscamos o valor do input na store e atribuimos a ele como value. E no evento de onChange fazemos o dispatch na action para mudar o estado do input.