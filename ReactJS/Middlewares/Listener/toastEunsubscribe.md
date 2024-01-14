# Toast e unsubscribe

Mudamos um pouco nosso middleware Listener:

    import { createStandaloneToast } from "@chakra-ui/toast";
    import { createListenerMiddleware } from "@reduxjs/toolkit";
    import categoriasService from "services/categorias";
    import { adicionarTodasAsCategorias, carregarCategorias } from "store/reducers/categorias";

    export const listener = createListenerMiddleware();

    const { toast } = createStandaloneToast();

    listener.startListening({
        actionCreator: carregarCategorias,
        effect: async (action, { dispatch, fork, unsubscribe }) => {
            toast({
                title: 'Carregando',
                description: 'Carregando categorias',
                status: 'loading',
                duration: 2000,
                isClosable: true
            });

            const tarefa = fork(async api => {
                await api.delay(1000);
                return await categoriasService.buscar();
            });

            const resposta = await tarefa.result;

            if (resposta.status === 'ok') {

                toast({
                    title: 'Sucesso!',
                    description: 'Categorias carregadas com sucesso!',
                    status: 'success',
                    duration: 2000,
                    isClosable: true
                });
                dispatch(adicionarTodasAsCategorias(resposta.value));
                unsubscribe();
            }

            if (resposta.status === 'rejected') {
                toast({
                    title: 'Erro',
                    description: 'Erro na busca de categorias',
                    status: 'error',
                    duration: 2000,
                    isClosable: true
                })
            }
        }
    });

Como podemos ver colocamos o a parte dos toasts aqui e não mais no reducer= de categorias e um ponto importante é que, toda vez que nós acessavamos a pagina Home, a plicaçao fazia uma chamada na api para carregar novamente as categorias, sendo que as categorias já foram carregadas uma vez, então no nosso if de sucesso utilizamos o unsubscribe():

    if (resposta.status === 'ok') {

        toast({
            title: 'Sucesso!',
            description: 'Categorias carregadas com sucesso!',
            status: 'success',
            duration: 2000,
            isClosable: true
        });
        dispatch(adicionarTodasAsCategorias(resposta.value));
        unsubscribe();
    }

Ou seja, caso a chamada da API já deu certo, 'ok', uma vez na aplicação ele para de ouvir o disparo daquela action, então não precisamos ficar buscando toda hora os dados na API, somente uma vez já basta o que traz performance na nossa aplicação.



