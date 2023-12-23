# Serviço GET de favoritos

Criamos algumas estilizações e criamos a parte de servicos dos favoritos aqui no frontend:

    import axios from 'axios'

    const favoritosApi = axios.create({
        baseURL: 'http://localhost:8000/favoritos'
    })

    async function getFavoritos() {
        const response = await favoritosApi.get('/')

        return response.data
    }

    export {
        getFavoritos,
    }

E também dentro da nossa página Favoritos.js utilizamos o useEffect:

    function Favorito() {

        const [ favoritos , setFavoritos ] = useState([])

        useEffect(() => {

            async function fetchFavoritos() {
                const favoritosDaAPI = await getFavoritos()
                setFavoritos(favoritosDaAPI)
            }

            fetchFavoritos()

        },[])

        return (
            <FavoritoContainer>
                {favoritos.map(favorito => (
                    <p>{favorito.nome}</p>
                ))}
            </FavoritoContainer>
        );
    }