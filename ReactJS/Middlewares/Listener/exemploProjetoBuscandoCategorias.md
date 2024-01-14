# Action carregarCategorias

Criamos uma nova action no reducer de categorias:

    export const carregarCategorias = createAction('categorias/carregarCategorias')

Criamos dessa forma, fora do reducer, assim também é outra forma de criar uma action.

Depois dentro do middleware de categorias:

    import { createListenerMiddleware } from "@reduxjs/toolkit";
    import { carregarCategorias } from "store/reducers/categorias";

    export const listener = createListenerMiddleware();

    listener.startListening({
        actionCreator: carregarCategorias,
        effect: async (action) => {
            console.log('Buscando categorias: ', action);
        }
    });

Vamos agora escutar essa action nova que criamos.

E dentro da page Home:

    useEffect(() => {
        dispatch(carregarCategorias());
        dispatch(buscarItens());
    }, [dispatch]);

Agora estamos fazendo o dispatch dessa nova action mas ainda não estamos buscando as categorias.

# Buscando categorias

Mudamos um pouco o arquivo categorias.js da pasta middlewares:

    import { createListenerMiddleware } from "@reduxjs/toolkit";
    import categoriasService from "services/categorias";
    import { adicionarTodasAsCategorias, carregarCategorias } from "store/reducers/categorias";

    export const listener = createListenerMiddleware();

    listener.startListening({
        actionCreator: carregarCategorias,
        effect: async (action, { dispatch , fork }) => {
            const tarefa = fork(async api => {
                return await categoriasService.buscar()
            });

            const resposta = await tarefa.result;

            if (resposta.status === 'ok') {
                dispatch(adicionarTodasAsCategorias(resposta.value))
            }
        }
    });

Aqui estamos usando o fork que ainda não entendi muito bem, mas com o tempo vou aprendendo.

Basicamente nós utilizamos o fork para que ele faça nossa busca na API e como sabemos o categoriasService.buscar() nos retorna todas as categorias da API.

Criamos uma const cahamada respota para sabermos o que aconteceu com a requisição na API.

Logo depois temos um if onde verificamos que caso o resposta.status for 'ok' podemos dar um disptach na action adicionarTodasAsCategorias e ela recebe no payload todas as categorias.

Agora no arquivo categorias.js do reducer nó criamos essa action:

    reducers: {
        adicionarTodasAsCategorias: (state, { payload }) => {
            return payload
        }
    }

Onde basicamente ele muda o estado de caetgorias com as categorias que vieram do payload.

Vamos estudar masi para frente que isso é uma boa maneira de lidar com o redux e dados na API, pois dessa forma podemos buscar na API somente os dados que precisamos naquela pagina/componente em específico, deixando nosso site com uma performance melhor. 
