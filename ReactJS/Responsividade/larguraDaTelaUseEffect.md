# Pegando largura da tela com useEffect()

Em alguns casos precisamos pegar a largura (width) da tela para conseguirmos fazer renderizações específicas de acordo com a largura da tela.

Tive um exemplo disso no desafio, onde eu queria renderizar uma coluna que fiz com display grid, dependendo da largura da tela. Dentro do componente fiz o seguinte:

    const [isSmallScreen, setIsSmallScreen] = useState(false);

    useEffect(() => {
        function handleResize() {
            setIsSmallScreen(window.innerWidth <= 740);
        }

        handleResize();
        window.addEventListener("resize", handleResize);

        return () => {
            window.removeEventListener("resize", handleResize);
        };
    });

Eu criei uma variável de estado para saber se a largura da tela seria menor ou igual a 740px. Se for retorna true se não retorna false.

Dentro do useEffect eu criei um addEventListener para escutar esse evento de redimensionar a tela. Lembrando que logo quando o componente renderiza o useEffect já chama a função handleResize() para sabermos o estado inicial da tela e depois caso tenha uma mudança de tela o código paga esse evento com o addEventListener. Lembrando que temos que remover esse addEventListener no return com removeEventListener, pois queremos que quando o componente for destruído ele destrua o addEventListener também, caso contrário pode dar algum tipo de problema.

Dessa forma no componente conseguimos fazer algo desse tipo:

    <HeaderContainer>
        {!isSmallScreen && <HomeText>Código</HomeText>}

        <HomeText>Descrição</HomeText>
        <HomeText>Valor</HomeText>
        <HomeText>Qtd</HomeText>
    </HeaderContainer>

Dessa forma a primeira parte só vai renderizar quando o width for maior que 740px, mas temos que lembrar de alterar o styled component também:

    export const HeaderContainer = styled.div `
        align-items: center;
        border-bottom: 1px solid white;
        color: #fff;
        display: grid;
        grid-template-columns: 20% 40% 10% 15% 15%;
        grid-template-rows: 1fr;
        height: 75px;
        justify-items: center;
        padding: .5rem;
        width: calc(100% - 10px);

        @media screen and (min-width: 741px) and (max-width: 1180px) {
            width: 100%;
        }

        @media screen and (max-width: 740px) {
            grid-template-columns: 45% 20% 20% 15%;
        }
    `

Com as midias conseguimos modificar também o grid de acordo com o width.
