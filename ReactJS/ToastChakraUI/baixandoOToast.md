# Baixando o Toast

Para evitar conflitos no projeto e a aula vamos intalar o Toast dessa forma:


    yarn add @chakra-ui/system@^2.3.0 @chakra-ui/toast@^4.0.0 @emotion/react@^11.10.5 @emotion/styled@^11.10.5 framer-motion@^7.6.2

Após fazer isso vamos no arquivo principal do nosso projeto que é o index.js e digitamos:

    import React from 'react';
    import ReactDOM from 'react-dom/client';
    import Router from 'routes';
    import './index.css';
    import store from './store';
    import { Provider } from 'react-redux';
    import { createStandaloneToast } from '@chakra-ui/toast'

    const { ToastContainer , toast } = createStandaloneToast()

    const root = ReactDOM.createRoot(document.getElementById('root'));
    root.render(
        <Provider store={store}>
            <Router />
            <ToastContainer />
        </Provider>
    );

    toast({
        description: 'está funcioando',
        duration: 2000
    })

Importamos o createStandaloneToast da nossa biblioteca e depois pegamos alguns compoonentes com:

    const { ToastContainer , toast } = createStandaloneToast()

Adicionamos o componente ToastContainer depois de router e fizemos uma configuração simples do toast logo abaixo:


    toast({
        description: 'está funcioando',
        duration: 2000
    })

Quando recarregamos a pagina aparece um Toast com a nossa mensagem e com a duração de 2 segundos.

