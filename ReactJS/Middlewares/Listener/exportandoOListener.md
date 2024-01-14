# Exportando o listener

Dentro do index.js da store deve conter somente o configureStore, então devemos criar um arquivo apenas para o listener.

Dentro da pasta store criamos uma pasta chamada middlewares e dentro dela um arquivo chamado categorias.js e nele digitamos:

    import { createListenerMiddleware } from "@reduxjs/toolkit";
    import { buscarCategorias } from "store/reducers/categorias";

    export const listener = createListenerMiddleware();

    listener.startListening({
        actionCreator: buscarCategorias.pending,
        effect: async (action) => {
            console.log('Buscando categorias: ', action);
        }
    });

E agora utilizamos apenas o listener no nosso arquivo index.js:

    import { configureStore } from '@reduxjs/toolkit';
    import categoriasSlice from './reducers/categorias';
    import itensSlice from './reducers/itens';
    import carrinhoSlice from './reducers/carrinho';
    import buscaSlice from './reducers/busca';
    import { listener } from './middlewares/categorias';

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