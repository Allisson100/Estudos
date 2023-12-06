# Utilizando o contexto

Primeiro é importante saber que o ideal é criar um pasta chamada context e dentro dela separar qual contexto é qual. Dentro da pasta criamos um arquivo chamado Usuario.js e nele digitamos:

    import { createContext , useState} from 'react'

    export const UsuarioContext = createContext();

    export const UsuarioProvider = ({ children }) => {

        const [nome , setNome] = useState("")
        const [saldo , setSaldo] = useState(0)

        return (
            <UsuarioContext.Provider value={{ nome, setNome, saldo, setSaldo }}>
                {children}
            <UsuarioContext.Provider >
        )
    }

E no nosso arquivo routes fazemos o seguinte:

    import { BrowserRouter , Switch , Route } from 'react-router-dom'
    import { UsuarioProvider } from context/Usuario.js

    function Router() {
        return (
            <BrowserRouter>
                <Switch>
                    <Route exact patch="/">
                        <UsuarioProvider>
                            <Login />
                        <UsuarioProvider>
                    </Route>
                <Switch>
            <BrowserRouter>
        )
    }

Dessa forma criamos um contexto para o usuario e apenas o nosso componente Login receberá o contexto.

Como sabemos todo contexto tem que ter um provider, entao dentro do nosso arquivo já criamos um componente com o provider dentro.

E para utilizarmos esse contexto na página Login:

    import { UsuarioContext } from 'context/Usuario.js'

    function Login() {

        const usuarioContext = useContext(UsuarioContext)
    }
