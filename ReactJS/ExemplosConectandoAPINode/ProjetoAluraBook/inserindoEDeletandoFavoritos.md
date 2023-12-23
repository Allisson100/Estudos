# Inserindo e deletando favoritos

Criamos agora a parte de adicionar o livro da Home ao ser clicado nos favoritos da seguinte forma:

    function Pesquisa() {
        const [livrosPesquisados, setLivrosPesquisados] = useState([])
        const [ livros , setLivros ] = useState([])

        useEffect(() => {

            async function fetchLivros () {
                const livrosDaApi = await getLivros()
                setLivros(livrosDaApi)
            }

            fetchLivros()
        }, [])

        async function insertFavorito(id) {
            await postFavoritos(id)
            alert('Livro inserido com sucesso!')
        }

        return (
            <PesquisaContainer>
                <Titulo>Já sabe por onde começar?</Titulo>
                <Subtitulo>Encontre seu livro em nossa estante.</Subtitulo>
                <Input
                    placeholder="Escreva sua próxima leitura"
                    onBlur={evento => {
                        const textoDigitado = evento.target.value
                        const resultadoPesquisa = livros.filter( livro => livro.nome.includes(textoDigitado))
                        setLivrosPesquisados(resultadoPesquisa)
                    }}
                />
                { livrosPesquisados.map( (livro , index) => (
                    <Resultado key={index} onClick={() => insertFavorito(livro.id)}>
                        <img src={livro.src} alt='Imagem'/>
                        <p>{livro.nome}</p>
                    </Resultado>
                ) ) }
            </PesquisaContainer>
        )
    }

    export default Pesquisa

Como podemos no onClick do componenete adiconamos a função assincrona para chamar a outra função assincrona await postFavoritos(id).

Agora vamos fazer a aparte de deletar.

Então no arquivo Favoritos.js:

    function Favorito() {

        const [ favoritos , setFavoritos ] = useState([])

        async function fetchFavoritos() {
            const favoritosDaAPI = await getFavoritos()
            setFavoritos(favoritosDaAPI)
        }

        useEffect(() => {

            fetchFavoritos()

        },[])

        async function deletarFavorito (id) {
            await deleteFavoritos(id)
            await fetchFavoritos()
            alert('Livro deletado com sucesso!')
        }

        return (
            <AppContainer>
                <div>
                    <Titulo>Aqui estão seus livros favoritos:</Titulo>
                    <ResultadoContainer>
                    {
                        favoritos.length !== 0 ? favoritos.map(favorito => (
                        <Resultado onClick={() => deletarFavorito(favorito.id)}>
                            <img src={livroImg} alt='Imagem'/>
                            <p>{favorito.nome}</p>
                        </Resultado>
                        )) : null
                    }
                    </ResultadoContainer>
                </div>
            </AppContainer>
        );
    }

    export default Favorito

Acrescentamos essa função:

    async function deletarFavorito (id) {
        await deleteFavoritos(id)
        await fetchFavoritos()
        alert('Livro deletado com sucesso!')
    }

O iteressante é que chamamos de novo a função  await fetchFavoritos() para atualizar o estado e atualizar a página de favoritos.