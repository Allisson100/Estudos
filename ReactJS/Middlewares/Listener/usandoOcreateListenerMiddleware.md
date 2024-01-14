# Usando o createListenerMiddleware

Começamos a configurar o nosso Middleware.

No arquivo index.js dentro da pasta store digitamos:

    import { configureStore , createListenerMiddleware } from '@reduxjs/toolkit';
    import categoriasSlice, { buscarCategorias } from './reducers/categorias';
    import itensSlice from './reducers/itens';
    import carrinhoSlice from './reducers/carrinho';
    import buscaSlice from './reducers/busca';

    const listener = createListenerMiddleware();

    listener.startListening({
        actionCreator: buscarCategorias.pending,
        effect: async (action) => {
            console.log('Buscando categorias: ', action);
        }
    });

    const store = configureStore({
        reducer: {
            categorias: categoriasSlice,
            itens: itensSlice,
            carrinho: carrinhoSlice,
            busca: buscaSlice,
        },
        middleware: getDefaultMiddleware => getDefaultMiddleware().prepend(listener.middleware),
    });

    export default store;

Primeiro criamos a const listener:

    const listener = createListenerMiddleware();

Depois criamos suas configurações:

    listener.startListening({
        actionCreator: buscarCategorias.pending,
        effect: async (action) => {
            console.log('Buscando categorias: ', action);
        }
    });

Primeiro temos que passar qual action queremos ouvir quando for disparada e também em qual estágio, pois como sabemos tem o estágio de pending, fulfilled e rejected, então no nosso caso ficou actionCreator: buscarCategorias.pending.

A segunda parte da configuração é o effect que é basicamente a ação que eu quero fazer quando eu ouvir essa action. Então passamos uma arrow function assincrona que apenas nos retorna um console log mostrando para gente o conteúdo da action disparada.

E por último temos uma configuração do configureStore para que o listener funcione:

    middleware: getDefaultMiddleware => getDefaultMiddleware().prepend(listener.middleware)

