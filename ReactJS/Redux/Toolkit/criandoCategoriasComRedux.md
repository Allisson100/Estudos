# Criando Categorias com Redux

# Criando categorias #2

Vamos começar instalando o redux no nosso projeto:

    yarn add @reduxjs/toolkit react-redux

Agora vamos criar uma nova pasta chamada store e dentro dela criar um arquivo chamado index.js. No arquivo index.js digitamos:

    import { configureStore } from '@reduxjs/toolkit'

    const store = configureStore({
        reducer: {

        }
    })

Antes de continuarmos vamos criar uma pasta chamada reducer onde vamos armazenar os reducer da store e ficar mais organizado. Dentro da pasta reducer vamos criar um arquivo chamado categorias.js e nele digitamos:

    import { createSlice } from '@reduxjs/toolkit'

    import automotivoThumb from 'assets/categorias/thumbnail/automotivo.png'
    import eletronicosThumb from 'assets/categorias/thumbnail/eletronicos.png'
    import escritorioThumb from 'assets/categorias/thumbnail/escritorio.png'
    import jogosThumb from 'assets/categorias/thumbnail/jogos.png'
    import somThumb from 'assets/categorias/thumbnail/som.png'

    import automotivoHeader from 'assets/categorias/header/automotivo.png'
    import eletronicosHeader from 'assets/categorias/header/eletronicos.png'
    import escritorioHeader from 'assets/categorias/header/escritorio.png'
    import jogosHeader from 'assets/categorias/header/jogos.png'
    import somHeader from 'assets/categorias/header/som.png'

    const estadoInicial = [
        {
            nome: 'Eletrônicos',
            thumbnail: eletronicosThumb,
            header: eletronicosHeader,
            id: 'eletronicos',
            descricao: 'Os melhores e mais atuais dispositivos eletrônicos estão aqui!'
        },
        { 
            nome: 'Automotivo',
            thumbnail: automotivoThumb,
            header: automotivoHeader,
            id: 'automotivos',
            descricao: 'Encontre aqui equipamentos para deixar seu carro com sua cara!'
        },
        { 
            nome: 'Jogos',
            thumbnail: jogosThumb,
            header: jogosHeader,
            id: 'jogos',
            descricao: 'Adquira os consoles e jogos mais atuais do mercado!'
        },
        { 
            nome: 'Escritório',
            thumbnail: escritorioThumb,
            header: escritorioHeader,
            id: 'escritorio',
            descricao: 'Tudo para que o seu escritório fique incrível!'
        },
        { 
            nome: 'Som e imagem',
            thumbnail: somThumb,
            header: somHeader,
            id: 'som',
            descricao: 'Curta suas músicas e seus filmes com a melhor qualidade!'
        }
    ] 

    const categoriasSlice = createSlice({
        name: 'categorias',
        initialState: estadoInicial,
    })

    // const categoriasSlice = createSlice({
    //     name: 'categorias',
    //     initialState // Caso a const do nosso array fosse o nome initialState também.
    // })

    export default categoriasSlice

Lembrando que agora estamos deixando o reducer com a responsabilidade das categorias, então tiramos a parte de categorias do nosso index Home.

Agora no arquivo index da store continuamos:

    import { configureStore } from '@reduxjs/toolkit'
    import categoriasSlice from 'reducers/categorias'

    const store = configureStore({
        reducer: {
            categorias: categoriasSlice
        }
    })

    export default store

E o arquivo categorias.js fica dessa forma o export:

    export default categoriasSlice.reducer

Agora precisamos comprtilhar essa store na nossa aplicação e para isso vamos no arquivo index proncipal da aplicação e digitamos:

    import React from 'react';
    import ReactDOM from 'react-dom/client';
    import Router from 'routes';
    import './index.css';

    import store from './store';
    import { Provider } from 'react-redux';

    const root = ReactDOM.createRoot(document.getElementById('root'));
    root.render(
        <React.StrictMode>
            <Provider store={store }>
                <Router />
            </Provider>
        </React.StrictMode>
    );

Porém agora na nossa página Home, categorias não existe mais, então temos que arrumar isso, pois agora categorias está na store, então digitamos:

    import Header from 'components/Header';
    import styles from './Home.module.scss';
    import relogio from 'assets/inicial.png';

    import { useNavigate } from 'react-router-dom';
    import { useSelector } from 'react-redux';


    export default function Home() {

        const navigate = useNavigate()

        const categorias = useSelector(state => state.categorias)

        return (
            <div>
                <Header
                    titulo='Classificados Tech'
                    descricao='Compre diversos tipos de produtos no melhor site do Brasil!'
                    imagem={relogio}
                    className={styles.header}
                />
                <div className={styles.categorias}>
                    <div className={styles['categorias-title']}>
                        <h1>
                            Categories
                        </h1>
                    </div>
                    <div className={styles['categorias-container']}>
                        {categorias.map((categoria , index) => (
                            <div key={index} onClick={() => navigate(`/categoria/${categoria.id}`)}>
                                <img src={categoria.thumbnail} alt={categoria.nome}/>
                                <h1>{categoria.nome}</h1>
                            </div>
                        ))}
                    </div>
                </div>
            </div>
        )
    }

Com essa linha de código ,  const categorias = useSelector(state => state.categorias), conseguimos obter o estado do nosso reducer.

O hook useSelector basicamente recebe uma arrow funtion que receb o conteúdo da store, mas nós devemos dizer extamente o que queremos pegar da store que no nosso caso é a parte de categorias, por isso utilizamos o store.categorias.

E é dessa forma que fazemos uma configuração incial do reducer.