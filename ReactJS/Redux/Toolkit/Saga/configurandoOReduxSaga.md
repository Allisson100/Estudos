# Configurando o Redux Saga

Dentro da pasta store criamos uma outra pasta chamada sagas e dentro dela um arquivo chamado categorias.js:

    import { takeEvery } from 'redux-saga/effects'
    import { buscarCategorias } from 'store/reducers/categorias'

    function* observarCategorias () {
        yield console.log('observando')
    }

    export function* categoriasSaga() {
        yield takeEvery(buscarCategorias, observarCategorias)
    }

Basicamente criamos uma funtion generator chamada observarCategorias e uma outra chamada categoriasSaga. Dentro de categoriasSaga utilizamos o yield junto com uma função chamada takeEvery(), essa função recebe como parâmetro a action que queremos obeservar e qual função rodar quando essa action for chamada que nesse caso é a observarCategorias que por enquanto apenas faz um console log.

Agora no arquivo index da store:

    import { configureStore } from '@reduxjs/toolkit';
    import categoriasSlice from './reducers/categorias';
    import itensSlice from './reducers/itens';
    import carrinhoSlice from './reducers/carrinho';
    import buscaSlice from './reducers/busca';
    import { categoriasListener } from './middlewares/categorias';
    import { itensListener } from './middlewares/itens';
    import createSagaMiddleware from 'redux-saga'
    import { categoriasSaga } from './sagas/categorias';

    const sagaMiddleware = createSagaMiddleware()

    const store = configureStore({
    reducer: {
        categorias: categoriasSlice,
        itens: itensSlice,
        carrinho: carrinhoSlice,
        busca: buscaSlice,
    },
    middleware:
        getDefaultMiddleware =>
        getDefaultMiddleware().prepend(
            categoriasListener.middleware,
            itensListener.middleware,
            sagaMiddleware
        ),
    });

    sagaMiddleware.run(categoriasSaga)

    export default store;

Nós primeiro ciramos um const: const sagaMiddleware = createSagaMiddleware().

Importamos o createSagaMiddleware do import createSagaMiddleware from 'redux-saga'.

Adicionamos também esse middleware saga junto com o do middlewareListener:

    middleware:
        getDefaultMiddleware =>
        getDefaultMiddleware().prepend(
            categoriasListener.middleware,
            itensListener.middleware,
            sagaMiddleware
        ),
    });

E por fim temos que rodas o nosso middleware categoriasSaga:

    sagaMiddleware.run(categoriasSaga)

Dessa forma toda vez que a action é disparada aparece no terminal o console.log('observando').