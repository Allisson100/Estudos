# react-router-dom

Resumo de codo usar uma biblioteca do React react-router-dom.

# Instalando o react-router-dom

Vamos utilizar a versão 6 do react-router-dom para esse video:

    npm i react-router-dom@6

# Criando o roteador

Adicionamos os componentes para criar as rotas, lembrando que estamos na versão 6 do react-router-dom:

    import { BrowserRouter, Route, Routes } from 'react-router-dom'
    import Inicio from './paginas/Inicio'
    import SobreMim from './paginas/SobreMim';

    function App() {
        return (
            <BrowserRouter>
                <Routes>
                    <Route path='/' element={<Inicio />}/>
                    <Route path='/sobremim' element={<SobreMim />}/>
                    <Route path='*' element={<h1>ERROOOO</h1>}/>
                </Routes>
            </BrowserRouter>
        );
    }

    export default App;

O path='\*' é como se fosse um coringa das rotas, ou seja, se por acaso alguma rota com qualuqer outro nome que não seja / ou /sobremim cairá em uma página de erro, normalmente a página 404.

# Links do react-router-dom

Criamos um componente menu dessa forma:

    import styles from './Menu.module.css'

    export default function Menu () {
        return (
            <header>
                <nav className={styles.navegacao}>
                    <a href="/" className={styles.link}>Inicio</a>
                    <a href="/sobremim" className={styles.link}>Sobre Mim</a>
                </nav>
            </header>
        )
    }

Porém vamos utilizar algumas ferramentas do react-router-dom para melhorar isso ficando assim:

    import { Link } from 'react-router-dom'
    import styles from './Menu.module.css'

    export default function Menu () {
        return (
            <header>
                <nav className={styles.navegacao}>
                    <Link to="/" className={styles.link}>Inicio</Link>
                    <Link to="/sobremim" className={styles.link}>Sobre Mim</Link>
                </nav>
            </header>
        )
    }

# Utilizando useLocation

Melhoramos o código do menu e utilizamos o hook que vem junto com a biblioteca react-router-dom que se chama useLocation():

Menu:

    import styles from './Menu.module.css'
    import MenuLink from '../MenuLink';

    export default function Menu () {

        return (
            <header>
                <nav className={styles.navegacao}>
                    <MenuLink to="/">Inicio</MenuLink>
                    <MenuLink to="/sobremim">Sobre Mim</MenuLink>
                </nav>
            </header>
        )
    }

MenuLink:

    import { Link, useLocation } from 'react-router-dom'
    import styles from './MenuLink.module.css'

    export default function MenuLink ({children , to}) {

        const localizacao = useLocation()

        return (
            <Link
                to={to}
                className={`${styles.link} ${localizacao.pathname === to && styles.linkDestacado}`}
            >
                {children}
            </Link>
        )
    }

# Utilizando rotas aninhadas

Aprendemos o conceito de rotas aninhadas.

Nosso arquivo routes.js ficou assim:

    import { BrowserRouter, Route, Routes } from 'react-router-dom'
    import Inicio from './paginas/Inicio'
    import SobreMim from './paginas/SobreMim';
    import Menu from './components/Menu';
    import Rodape from 'components/Rodape';
    import PaginaPadrao from 'components/PaginaPadrao';

    function AppRoutes() {
        return (
            <BrowserRouter>

            <Menu />

            <Routes>
                <Route path='/' element={<PaginaPadrao />}>
                    <Route path='/' element={<Inicio />}/>
                    <Route path='/sobremim' element={<SobreMim />}/>
                </Route>

                <Route path='*' element={<h1>ERROOOO</h1>}/>
            </Routes>

            <Rodape />
            </BrowserRouter>
        );
    }

    export default AppRoutes;

Criamos essa rota aninhada:

    <Route path='/' element={<PaginaPadrao />}>
        <Route path='/' element={<Inicio />}/>
        <Route path='/sobremim' element={<SobreMim />}/>
    </Route>

Basicamente conseguimos criar um layout padrão para ambas as rotas, porém com conteúdos diferentes entre elas. Nosso arquivo da PaginaPadrao está assim:

    import Banner from "components/Banner";
    import { Outlet } from "react-router-dom";

    export default function PaginaPadrao () {
        return (
            <main>
                <Banner />

                <Outlet />
            </main>
        )
    }

A tag <Outlet /> serve justamente para renderizar os conteúdos específicos de cada tag.

O arquivo index do Inicio está assim:

    import styles from './Inicio.module.css'
    import Post from 'components/Post';

    import posts from 'json/posts.json'

    export default function SobreMim () {
        return (
            <ul className={styles.posts}>
                {posts.map((post) =>(
                    <li key={post.id}>
                        <Post post={post}/>
                    </li>
                ))}
            </ul>
        )
    }

É como se além do layout padrão, o react vai adicionar esse código da página Inicio.

# Utilizando useParams

Renomeamos o componente Post para PostCard, pois agora eu quero utilizar o nome Post para outro componente. Nele será renderizado o conteúdo de cada noticia que temos na página inicial do projeto.

O arquivo post está assim por enquanto:

    import { useParams } from "react-router-dom"

    export default function Post () {

        const parametros = useParams()
        console.log(parametros);

        return (
            <h1>Posts {parametros.id}</h1>
        )
    }

Utilizamos um dos hooks do react-router-dom para saber qual é o id que está na rota.

E envolvemos cada PostCard em Links do react-router-dom:

    import { Link } from 'react-router-dom'
    import styles from './Post.module.css'

    export default function PostCard ({ post }) {
        return (
            <Link to={`/posts/${post.id}`}>
                <div className={styles.post}>
                    <img
                        className={styles.capa}
                        src={`/assets/posts/${post.id}/capa.png`}
                        alt="Imagem de capa do post"
                    />

                    <h2 className={styles.titulo}>{post.titulo}</h2>

                    <button className={styles.botaoLer}>Ler</button>
                </div>
            </Link>
        )
    }

E também adicionamos uma nova rota:

    function AppRoutes() {
        return (
            <BrowserRouter>

            <Menu />

            <Routes>
                <Route path='/' element={<PaginaPadrao />}>
                    <Route index element={<Inicio />}/>
                    <Route path='sobremim' element={<SobreMim />}/>
                    <Route path='posts/:id' element={<Post />}/>
                </Route>

                <Route path='*' element={<h1>ERROOOO</h1>}/>
            </Routes>

            <Rodape />
            </BrowserRouter>
        );
    }

# Elemento Posts

Basicamente pegamos o id da rota atrvés do useParams e assim conseguimos filtrar o post pelo id e mostrar o post adequado para aquela rota especifica e eutilizamos a biblioteca do mrkdown para editar o texto.

Vamos instalar e utilizar o react-markdown para nos ajudar na parte do texto, pois queremos mostrar titulo, links e outras coisas presentes no texto e a markdown pode no ajudar com isso.

Para instalá-la digitamos:

    npm install react-markdown

Utilizamos ela da seguinte forma

    import './Post.css'

    import { useParams } from "react-router-dom"
    import posts from 'json/posts.json'
    import PostModelo from "components/PostModelo"

    import ReactMarkdown from 'react-markdown'

    export default function Post () {

        const parametros = useParams()
        const post = posts.find((post) => {
            return post.id === Number(parametros.id)
        })

        return (
            <PostModelo
                fotoCapa={`/assets/posts/${post.id}/capa.png`}
                titulo={post.titulo}
            >
                <div className="post-markdown-container">
                    <ReactMarkdown>
                        {post.texto}
                    </ReactMarkdown>
                </div>
            </PostModelo>
        )
    }

Nós utilizamos um componente que da biblioteca e colocamos ele entre o texto em markdown.

Com o texto em markdown não conseguimos aplicar classes para eles, então por isso devemos utilizar um arquivo css padrão, pois desse jeito ele pode ser utilizado globalmente vamos dizer assim. E quando o texto for convertido de markdown para as tags html, essas tags vão pegar a estilização.

# Utilizando useNavigate

Por enquanto apenas criamos um componente BotaoPrincipal para não ter repetição de código.

    const navegar = useNavigate()

Utilizamos esse hook para conseguirmo navegar pelas nossas rotas.

    <div
        className={styles.botaoContainer}
        onClick={() => navegar(-1)}
    >
        <BotaoPrincipal tamanho="lg">Voltar</BotaoPrincipal>
    </div>

Nos utilizamos dessa maneira, pois no onClick ele irá redirecionar para a página anterios, isso utilizando o -1 e poderiamos voltar duas páginas utilizando o -2 e também podemos usar da seguinte forma:

    onClick={() => navegar("/")}

Dessa forma ele redireciona para a rota "/", então podemos usar tanto as rotas que criamos como números.
