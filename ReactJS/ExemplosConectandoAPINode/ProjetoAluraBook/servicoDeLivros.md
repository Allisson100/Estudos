# Serviço de livros na Home

Agora sim conectamos nosso FrontEnd com o BackEnd.

No componente Pesquisa arrumas o useEffect:

    useEffect(() => {

        async function fetchLivros () {
            const livrosDaApi = await getLivros()
            setLivros(livrosDaApi)
        }

        fetchLivros()

    }, [])

Pois como sabemos requisições são assincronas e é dessa forma que utilizamos funções assincronas no useEffect.

Também arrumamos a função do getLivros em nosso servicos:

    import axios from 'axios'

    const livrosApi = axios.create({
        baseURL: 'http://localhost:8000/livros'
    })

    async function getLivros() {
        const response = await livrosApi.get('/')

        return response.data
    }

    export {
        getLivros,
    }

E alteramos uma coisa em nosso código do BackEnd.

No arquivo app.js acrescentamos o cors:

    const express = require('express')
    const rotaLivro = require('./rotas/livros')
    const cors = require('cors')

    const app = express()
    app.use(express.json())
    app.use(cors({origin: '*'}))

    app.use('/livros', rotaLivro )


    const port = 8000

    app.listen(port, () => {
        console.log(`App running, port: ${port}`);
    })

Por segurança a nossa aplicação frontend não pode simplesmente fazer uma requisição em nosso servidor, enbtão devemos utilizar a biblioteca cors para nos ajudar controlar quem pode e quem não pode acessar nossa aplicação.

Nesse caso configuramos ele com um '*', pois como é apenas um servidor de estudos, qualuqer um pode acessar.

Caso quisermos dar acesso a uma url especifica podemos fazer assim:

    app.use(cors({origin: 'http://localhost:3001'}))
