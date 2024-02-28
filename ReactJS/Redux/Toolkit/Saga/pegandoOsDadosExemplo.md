# Pegando os dados

Nós criamos a seguinte estrutura na parte de pagamentos:

import { call, takeLatest } from "redux-saga/effects";
import bandeirasService from "services/bandeiras";
import cartoesService from "services/cartoes";
import usuariosServices from "services/usuarios";
import { carregarPagamento } from "store/reducers/carrinho";

    const usuarioLogado = 1

    function* carregarPagamentoSaga() {
        try {
            const usuario = yield call(usuariosServices.buscarPorId, usuarioLogado)
            const cartoes = yield call(cartoesService.buscarPorIdUsuario, usuarioLogado)
            const banderiasIds = cartoes.map(cartao => cartao.bandeiraId)
            const bandeiras = yield call(bandeirasService.buscarPorId, banderiasIds)
            const cartoesComBandeiras = cartoes.map(cartao => {
                const bandeiraDoCartao = bandeiras.find(bandeira => bandeira.id === cartao.bandeiraId)
                return { ...cartao, taxa: bandeiraDoCartao.taxa, bandeira: bandeiraDoCartao.nome }
            })

            console.log({ ...usuario, cartoes: cartoesComBandeiras });
        } catch (error) {

        }
    }

    export function* carrinhoSaga () {
        yield takeLatest(carregarPagamento, carregarPagamentoSaga)
    }   

Primeiro simulamos um usuário logado: const usuarioLogado = 1.

Depois criamos uma lógica para obter um objeto onde teremos o nome do usuário e também os cartões dele.

Lembrando que toda vez que utilizamos o service é uma requisição para API.

    const usuario = yield call(usuariosServices.buscarPorId, usuarioLogado)
    const cartoes = yield call(cartoesService.buscarPorIdUsuario, usuarioLogado)

Nesses exemplos utilizamos o call com dois parâmetros, pois a função buscarPorId precisa do parâmetro id para fazer a busca e quando utilizamos uma function generator devemos passar o parâmetro dessa forma.

### Para saber mais sobre o código que acabamos de fazer

    import { all, call } from 'redux-saga/effects';

    const [usuario, cartoes, bandeiras] = yield all([
        call(usuariosService.buscarPorId, usuarioLogado),
        call(cartoesService.buscarPorIdUsuario, usuarioLogado),
        call(bandeirasService.buscarPorIdUsuario, usuarioLogado)
    ]);

Isso aqui funcionaria igual.

A forma de fazer o saga roda sem o all:

    sagaMiddleware.run(categoriasSaga);
    sagaMiddleware.run(carrinhoSaga);

Com o All:

    function* rootSaga() {
        yield all([
            categoriasSaga(),
            carrinhoSaga()
        ])
    }

    sagaMiddleware.run(rootSaga);

Dessa forma temos um código mais conciso.