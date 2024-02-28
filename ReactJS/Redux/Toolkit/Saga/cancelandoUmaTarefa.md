# Cancelando uma tarefa

Ainda temos um problema. Quando entramos no site as categorias são carregadas normalmente, porém se a agente mudar de aba e voltar para a tela inicial novamente vamos ver que as categorias serão carregadas novamente e temos que mudar isso.

    export function* categoriasSaga() {
        const tarefa = yield takeLatest(carregarCategorias, observarCategorias)

        yield takeLatest(adicionarTodasAsCategorias, () => tarefa.cancel())
        // yield takeLatest(adicionarTodasAsCategorias, function*() {yield cancel(tarefa)})
    }

Agora utilizamos o takeLatest, pois significa que após a última execução de uma action faça alguma coisa. O takeLatest é mais utilizado que takeEvery, pois o takeEvery toda hora que acontecer uma chamada na action, ele vai executar a function worker todas as vezes, ou seja, se for chamada 10 vezes então vai executar 10 vezes a função. Já o takeLatest, mesmo que a action seja disparada 10 vezes, será executada somente 1 vez a função woker.

E aqui utilizamos:

    yield takeLatest(adicionarTodasAsCategorias, () => tarefa.cancel())

Para que na última chamada da action cancele ela, dessa forma carrega as categorias somente uma vez.

E exeiste outra forma de fazer que é assim:

    yield takeLatest(adicionarTodasAsCategorias, function*() {yield cancel(tarefa)})

Ambas as formas estão corretas e funcionam.