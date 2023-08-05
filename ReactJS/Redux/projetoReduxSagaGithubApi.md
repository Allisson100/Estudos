Projeto na pasta Github/Testes/apiGithubRedux

# Explicando o Redux Saga pra pedir requisição para a API do GitHub

Primeiro para configurar o Redux Saga temos que criar a estrutra de pastas dentro da pasta src.

    store
        modules
            pasta_com_nome_referente_a_usabilidade

- store: além das pasta contém os arquivos: createStore.ts e index.ts
- modules: além da pasta contém os arquivos: rootReducer.ts e rootSaga.ts
- pasta_com_nome_referente_a_usabilidade contém os arquivos: actions.ts , reducer.ts , sagas.ts, types.ts

### Conexão com API

Arquivo de conexão com a API, githubApi.ts:

    export default async function githubApi (user: string) {
        try {
            const response = await fetch(`https://api.github.com/users/${user}`)

            console.log(response);

            if (response.ok === false) {
                throw new Error('Failed to fetch user');
            }

            const data = await response.json()

            return data
        } catch (error) {
            console.log(error);
        }
    }

Aqui nesse arquivo fazemos o fetch normal na api e podemos usar o axios caso necessário, lembrando que devemos passar a rota necessária para acessar a api corretamente se usarmos o axios na action githubUserRequest.

### actions.ts

Arquivo actions.ts:

    import { action } from 'typesafe-actions'

    interface Props {
        user: string;
    }

    interface githubUserData {
        url: string;
        loginName: string;
        numberPublicRepo: number;
        bio: string;
    }

    export function githubUserRequest({ user }: Props ) {
        return action ('@gitHubUser/GITHUB_USER_REQUEST', {
                    user,
                })
    }

    export function githubUserSuccess({ url ,loginName , numberPublicRepo , bio }: githubUserData ) {
        return action ('@gitHubUser/GITHUB_USER_SUCCESS', {
            url,
            loginName,
            numberPublicRepo,
            bio,
        })
    }

    export function githubUserFailure() {
        return action ('@gitHubUser/GITHUB_USER_FAILURE')
    }

Nesse caso estamos usando uma única api que é a API do github, primeiro temos a action referente a chamada da API, temos a action para quando a API conseguir buscar os dados com sucesso e também temos a action para sabermos se a API falhou ao buscar os dados.

##### ACTION githubUserRequest

export function githubUserRequest({ user }: Props ) {
return action ('@gitHubUser/GITHUB_USER_REQUEST', {
user,
})
}

Essa action serve para dizermos que queremos utilizar a API, temos que passar o user como payload, pois utlizamos a variável user no link de requisição, para conseguirmos buscar users diferente.

### ACTION githubUserSuccess

    export function githubUserSuccess({ url ,loginName , numberPublicRepo , bio }: githubUserData ) {
            return action ('@gitHubUser/GITHUB_USER_SUCCESS', {
                url,
                loginName,
                numberPublicRepo,
                bio,
            })
        }

Essa action serve para que em caso de sucesso com a conexão da API ela nos retorne apenas os dados que queremos e nesse caso podemos utilizar qualquer nome, vamos definir essas variáveis corretamente depois.
Lembrando que essas quatro variáveis são o payload.

### ACTION githubUserFailure

    export function githubUserFailure() {
            return action ('@gitHubUser/GITHUB_USER_FAILURE')
        }

Essa action serve apenas para saber se a conexão da API deu falha ou não por isso não temos payload.

E claro que em todas essas actions tem que ser tipadas.

### reducer.ts

Após as actions temos uma ramificação, temos o Saga trabalhando nesse momentoe também o reducer. Vamos explicar o Reducer primeiro.

Arquivo reducer.ts:

    import { GithubUserActions , GithubUserState } from './types'

    const initialState: GithubUserState = {
        data: {
            url: '',
            loginName: '',
            numberPublicRepo: 0,
            bio: 'string',
        },
        loadingGithubUserRequest: false,
        didGetUser: false,
        error: false,
    }

    export default function githubUser(state = initialState, action: GithubUserActions): GithubUserState {
        switch (action.type) {
            case '@gitHubUser/GITHUB_USER_REQUEST':
                return {
                    ...state,
                    loadingGithubUserRequest: true,
                }
            case '@gitHubUser/GITHUB_USER_SUCCESS':
                return {
                    ...state,
                    data: action.payload,
                    didGetUser: true,
                    loadingGithubUserRequest: false,
                    error: false,
                }
            case '@gitHubUser/GITHUB_USER_FAILURE':
                return {
                    ...state,
                    loadingGithubUserRequest: false,
                    error: true,
                    didGetUser: false,
                }

            default:
                return state
        }
    }

Primiero temos que falar da tipagem, temos duas tipagens diferentes aqui, uma para action e uma para os valores iniciais.

Arquivo type.ts:

    import { ActionType } from "typesafe-actions"
    import * as actions from './actions'

    export type GithubUserActions = ActionType<typeof actions>

    export interface GithubUserState {
        readonly data: {
            url: string;
            loginName: string;
            numberPublicRepo: number;
            bio: string;
        },
        readonly didGetUser: boolean,
        readonly loadingGithubUserRequest: boolean;
        readonly error: boolean;
    }

Aqui temos a interface do estado inicial que chamamos de GithubUserState e também temos o GithubUserActions que atribuimos para ele o ActionType que vem de uma biblioteca que instalamos para melhorar a inteligencia de nosso código.

Voltando para o arquivo reducer.ts podemos ver que temos uma função chamada githubUser e nela passamos dois parâmetros o state = initialState e também action. Temos que tipar as action e o state já está tipado, pois a nossa initialState já está tipado. Temos que tipar também o retorno dessa função que também vai possuir os valores de uma de nossas initialState.

Depois temos uma estutura de switch case que é basicamente um if else, mas no caso do reducer é mais organizado e mais utilizado a estrutura switch case.

Dentro dela precisamos criar o que queremos de alteração de variáveis dependendo da action que ativarmos.

    case '@gitHubUser/GITHUB_USER_REQUEST':
                return {
                    ...state,
                    loadingGithubUserRequest: true,
                }

Nesse caso precisamos que quando alguma parte do código chamar a API do github, nossa variável de loadig chamada loadingGithubUserRequest seja TRUE, pois com essa afirmação podemos criar um componente de loading por exemplo.

    case '@gitHubUser/GITHUB_USER_SUCCESS':
                return {
                    ...state,
                    data: action.payload,
                    didGetUser: true,
                    loadingGithubUserRequest: false,
                    error: false,
                }

Nesse outro case, caso a requisição na API for um sucesso temos que obter os dados que queremos da API, precisamos dizer se houve a busca do usuário com a variável didGetUser, essa variável é semelhante com uma variável comum chamada isSigned para sabermos se o usuário efetuou com sucesso o login, temos também que mudar o estado do loading para falso, pois o careegamento já foi feito, e também temos que dizer que a variável erro foi falsa.

    case '@gitHubUser/GITHUB_USER_FAILURE':
                return {
                    ...state,
                    loadingGithubUserRequest: false,
                    error: true,
                    didGetUser: false,
                }

Nesse outro caso temos a situação em que o requisição da API falha, que na verdade acontece quando nenhum usuário é encontrado na api do github. Vale lembrar que caso tenha um erro de conexão na própria API, ou seja, não conseguimos ter retorno se existe usuário ou não na API, eu estou utilizando um throw lá na parte da requisição da api e ai o código printa no console o erro.

### Sagas

No arquivo sagas.ts temos:

    import { takeLatest , call , put , all } from "redux-saga/effects";
    import { ActionType } from 'typesafe-actions'
    import * as actions from './actions'

    import githubApi from "../../../services/githubApi";

    interface GithubApiResponse {
        avatar_url: string;
        login: string;
        public_repos: number;
        bio: string;
    }

    export function* getGithubUser({ payload }: ActionType<typeof actions.githubUserRequest>) {
        try {

            const { user } = payload

            // yield delay(10000)

            const data: GithubApiResponse = yield call(githubApi, user)

            yield put(actions.githubUserSuccess({
                url: data.avatar_url,
                loginName: data.login,
                numberPublicRepo: data.public_repos,
                bio: data.bio,
            }))

        } catch (error) {
            yield put(actions.githubUserFailure())
        }
    }

    export default all ([
        takeLatest('@gitHubUser/GITHUB_USER_REQUEST', getGithubUser)
    ])

Esse arquivo é a parte paralela que funciona ao mesmo tempo que o reducer. Utilizamos o Saga, pois o redux com a estrutura padrão não no permite trazer side effects e um dos side effects que ele desabilita é a requisição da API, por isso temos o SAGA e o THUNK para utilarmos, mas o THUNK não é muito utilizado mais por problemas passados.

Nesse arquivo temos uma função generator(estudar depois) que é representado com function\* e nela podemos usar o yield.

É nessa parte que vamos buscar os nossos dados na API e salvá-los na store do redux.

Como vamos fazer uma requisição é interesante utilizar try e catch.

Precisamos desestruturar a variável user do payload, mais para frente vamos entender melhor isso. A const data é a constante que vai recebr todos os dados da API e nele utilizamos o yield com a função call para chamar a função e passamos para a função da api a variável user. Vale lembrar que caso usarmos o axios, podemos passar um terceiro parâmetro que seria o restante da rota para pegar algum dado específico da API, mas nesse caso dentro da função call chamar a função da api e passar a variável user que precisamos já é o necessário.

Depois que temos a variável data com todas as informações precisamos filtrar esses dados e pegar somente o que precisamos utilzar.

Vale ressaltar que o SAGA é uma função paralela, mas depois dela ela faz o caminho do reducer de novo, pois precisamos filtrar os dados.

    yield put(actions.githubUserSuccess({
                url: data.avatar_url,
                loginName: data.login,
                numberPublicRepo: data.public_repos,
                bio: data.bio,
            }))

Depois de termos o dados na const data, temos que chamar a yield put, pois lembrar que definimos algumas variáveis na função da action githubUserSuccess, então é agora que configuramos ela.

Apenas para lembrar action githubUserSuccess:

    export function githubUserSuccess({ url ,loginName , numberPublicRepo , bio }: githubUserData ) {
        return action ('@gitHubUser/GITHUB_USER_SUCCESS', {
            url,
            loginName,
            numberPublicRepo,
            bio,
        })
    }

Voltando ao arquivo saga.ts no yield put fazemos a relação dos nomes lá da action com os nomes reais da api.

Depois na parte do catch apenas chamamos a action githubUserFailure, pois pode ocorrer de termos um erros e isso vai chamar essa action que vai ativar o case do reducer @gitHubUser/GITHUB_USER_FAILURE e com isso mudar a variável error para true.

E por fim utilizamos essa estrutura de exportação:

    export default all ([
        takeLatest('@gitHubUser/GITHUB_USER_REQUEST', getGithubUser)
    ])

Aqui utilizamos o takeLatest, pois queremos sempre o últimos estados das variáveis e fazemos a relação da action @gitHubUser/GITHUB_USER_REQUEST com essa função do saga getGithubUser.

Lembrando que é essa função que vamos chamar no dispach quando precisarmos.

### Types

Arquivo types.ts:

    import { ActionType } from "typesafe-actions"
    import * as actions from './actions'

    export type GithubUserActions = ActionType<typeof actions>

    export interface GithubUserState {
        readonly data: {
            url: string;
            loginName: string;
            numberPublicRepo: number;
            bio: string;
        },
        readonly didGetUser: boolean,
        readonly loadingGithubUserRequest: boolean;
        readonly error: boolean;
    }

Eu já tinha colocado esse código na parte de reducer, mas coloquei de novo pra organização, é apenas a tipagem do initialState e das actions.

### Pasta modules arquivo rootReducer e rootSaga

Arquivo rootReducer:

    import { combineReducers } from 'redux'
    import githubUser from './github/reducer'
    import { StoreState } from '../createStore'

    export default combineReducers<StoreState>({
        githubUser,
    })

Não temos muito o que explicar aqui. Esse arquivo é apenas para juntar todos os reducer existentes no projeto.

único detalhe aqui é a tipagem StoreState que vamos ver depois, pois ele vem de outro arquivo.

Arquivo rootSaga:

    import getGithubUser from './github/sagas'
    import { all } from 'redux-saga/effects'

    export default function* rootSaga() {
        yield all([getGithubUser])
    }

Aqui temos a junção de todos os sagas que vamos utilizar no projeto.

### Mais funcionalidades

Se tiver mos mais de uma funcionalidade no projeto é nesses dois arquivos que vamos juntar tudo, por exemplo caso utilizarmos a api do giuthub e do twitter.

O arquivo rootReducer ficaria assim:

    import { combineReducers } from 'redux';
    import githubReducer from './github/reducer';
    import twitterReducer from './twitter/reducer';

    const rootReducer = combineReducers({
        github: githubReducer,
        twitter: twitterReducer,
    });

    export default rootReducer;

E o arquivo rootSaga assim:

import { all } from 'redux-saga/effects';
import githubSaga from './github/sagas';
import twitterSaga from './twitter/sagas';

    function* rootSaga() {
        yield all([
            githubSaga(),
            twitterSaga(),
            // ... outras sagas
        ]);
    }

    export default rootSaga;

### Arquivos createStore e index

Esses próximos arquivos são mais para configuração.

Arquivo createStore:

    import { applyMiddleware, createStore, Middleware } from 'redux';
    import createSagaMiddleware from 'redux-saga';
    import rootReducer from './modules/rootReducer';
    import rootSaga from './modules/rootSaga';
    import { GithubUserState } from './modules/github/types';

    export interface StoreState {
        githubUser: GithubUserState;
    }

    const sagaMiddleware = createSagaMiddleware();

    const middlewares: Middleware[] = [sagaMiddleware];

    const store = createStore(rootReducer, applyMiddleware(...middlewares));

    sagaMiddleware.run(rootSaga);

    export default store;

Como o próprio nome diz é aqui que criamos a store. O que não podemos esquecer é caso utilzarmos outras funcionalidades temos que atualizar a interface StoreState.

Arquivo index.ts:

    import { applyMiddleware, createStore, Middleware } from 'redux'
    import createSagaMiddleware from 'redux-saga'
    import rootReducer from './modules/rootReducer'
    import rootSaga from './modules/rootSaga'

    const sagaMiddleware = createSagaMiddleware()
    const middlewares: Middleware[] = [sagaMiddleware]
    const store = createStore(rootReducer, applyMiddleware(...middlewares))

    sagaMiddleware.run(rootSaga)

    export { store };

Não tem muito o que falar, faz parte da criação da store também.
