# Criando saga de carrinho

Dentro da pasta sagas da pasta store criamos um arquivo chamado carrinho.js:

    import { takeLatest } from "redux-saga/effects";
    import { carregarPagamento } from "store/reducers/carrinho";

    function* carregarPagamentoSaga() {
        yield console.log('Carregando pagamento');
    }

    export function* carrinhoSaga () {
        yield takeLatest(carregarPagamento, carregarPagamentoSaga)
    }

Como sempre temos o watcher e o worker e nesse caso quando página Pagamentos disparar a action carregarPagamentoSaga:

    useEffect(() => {
        dispatch(carregarPagamento)
    }, [dispatch])

O watcher vai fazer com que a função worker faça o log no terminal.

Não podemos esquecer de acrescentar a função whatcher lá no arquivo index da store.

    sagaMiddleware.run(carrinhoSaga)

E também não podemos esquecer de criar essa action no arquivo dentro da pasta reducers chamado carrinho.js:

    export const carregarPagamento = createAction('carrinho/carregarPagamento')

