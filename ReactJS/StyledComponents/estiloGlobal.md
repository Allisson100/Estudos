# Estilo Global com Styled Component

Primeiro precisamos instalar:

    yarn add styled-components

Para criar um estilo global com as formatações precisamos criar uma pasta dentro da pasta src com o nome styles e dentro da pasta styles criar um arquivo chamado global.js ou global.ts e nele digitamos:

    import { createGlobalStyle } from 'styled-components'

    export default createGlobalStyle `
        * {
            box-sizing: border-box;
            margin: 0;
            outline: 0;
            padding: 0;
        }

        #root {
            height: 100vh;
            padding: 1rem;
            width: 100%;

            @media screen and (max-width: 1180px) {
                height: 100%;
            }
        }

        body {
            background-color: #1e1e1e;
        }
    `

E para usar esse estilo global, dentro do arquivo principal do projeto no meu caso App.jsx digitamos:

    import GlobalStyles from "./styles/global";
    import Home from "./pages/Home";

    function App() {
    return (
        <>
        <GlobalStyles />
        <Home />
        </>
    );
    }

    export default App;

Importamos o GlobalStyles e utilizamos ele no componente.
