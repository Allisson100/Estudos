# Chamando a api

import { call, delay, put, takeEvery } from 'redux-saga/effects'
import { adicionarTodasAsCategorias, carregarCategorias } from 'store/reducers/categorias'
import { createStandaloneToast } from '@chakra-ui/toast';
import categoriasService from 'services/categorias';

    const { toast } = createStandaloneToast();

    function* observarCategorias () {
        yield console.log('observando')

        toast({
            title: 'Carregando',
            description: 'Carregando categorias',
            status: 'loading',
            duration: 2000,
            isClosable: true
        });

        try {
            yield delay(1000)
            const categorias = yield call(categoriasService.buscar)
            yield put(adicionarTodasAsCategorias(categorias))

            toast({
                title: 'Sucesso!',
                description: 'Categorias carregadas com sucesso!',
                status: 'success',
                duration: 2000,
                isClosable: true
            });
        } catch (error) {
            toast({
                title: 'Erro',
                description: 'Erro na busca de categorias',
                status: 'error',
                duration: 2000,
                isClosable: true
            }); 
        }
    }

    export function* categoriasSaga() {
        yield takeEvery(carregarCategorias, observarCategorias)
    }

Aqui nessse primiero lançamos o toast de carregando e depois disso temos que averiguar se realmente conseguimos buscar os daddos da api ou não e para isso utilizamos o try catch.

    try {
        yield delay(1000)
        const categorias = yield call(categoriasService.buscar)
        yield put(adicionarTodasAsCategorias(categorias))

        toast({
            title: 'Sucesso!',
            description: 'Categorias carregadas com sucesso!',
            status: 'success',
            duration: 2000,
            isClosable: true
        });
    }

No bloco try primeiro colocamos um delay apenas para simular um demora de 1s.

Depois chamamos a função buscar de categoriasService:

    buscar: async () => {
        const resposta = await instance.get('/categorias');

        return resposta.data;
    },

Nada mais é que uma chamada comum em uma api utilizando o axios.

Depois através do slicer de categorias passamos atrvés do payload para adicionarTodasAsCategorias as próprias categorias que por sua vez irá atualizar o estado de categorias e renderizar na tela.

E por fim temos o bloco catch:

    catch (error) {
        toast({
            title: 'Erro',
            description: 'Erro na busca de categorias',
            status: 'error',
            duration: 2000,
            isClosable: true
        }); 
    }

Caso de algum erro na requisição da api e cai nesse bloco.