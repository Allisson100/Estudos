# Contexto de Carrinho

Criamos um contexo interessante para administrar o carrinho de pagamento da página. Então criamos um arquivo novo chamada Carrinho.js na pasta contexts:

    import { createContext, useContext, useState } from 'react';

    export const CarrinhoContext = createContext();
    CarrinhoContext.displayName = "Carrinho";

    export const CarrinhoProvider = ({ children }) => {

        const [carrinho , setCarrinho] = useSatet([]);

        return (
            <CarrinhoContext.Provider value={{ carrinnho , setCarrinho }}>
                {children}
            </CarrinhoContext.Provider>
        )

    }

    export const useCarrinhoContext = () => {

        const { carrinho , setCarrinho } = useContext(CarrinhoContext)

        function adicionarProduto(novoProduto) {

            const temOProduto = carrinho.some(itemDoCarrinho => intemDoCarrinho.id === novoProduto.id)

            if(!temOProduto) {
                novoProduto.quantidade = 1

                return setCarrinho(carrinhoAnterior => [...CarrinhoAnterior, novoProduto])
            }

            setCarrinho(carrinhoAnterior => carrinhoAnterior.map(itemCarrinho => {
                if (itemCarrinho.id === novoProduto.id) itemCarrinho.quantidade += 1
                return itemCarrinho
            }))
        }

        return (
            carrinho,
            setCarrinho,
            adicionarProduto
        )
    }

Componente do Produto em si fica assim:

    const {carinho , adicionarProduto} = useCarrinhoContext()

    const produtoNoCarrinho = carrinho.find(itemDoCarrinho => intemdoCarrinho.id === id)


    <ComponenteBotaoAdicionar
        onClick={() => adicionarProduto({nome, foto , id valor})}
    >
        {produtoNoCarrinho.qunatidade || 0}
    <ComponenteBotaoAdicionar>

### Explicação

Como podemos ver dentro do nosso arquivo de contexto do carrinho, além do contexto criamos também um hook personalizado, pois o componente em si do produto não tem responsabilidade de saber como devemos adicinar o produto no carrinho, isso fica como função do contexto. Então basicamente:

    export const useCarrinhoContext = () => {

        const { carrinho , setCarrinho } = useContext(CarrinhoContext)

        function adicionarProduto(novoProduto) {

            const temOProduto = carrinho.some(itemDoCarrinho => intemDoCarrinho.id === novoProdutor.id)

            if(!temOProduto) {
                novoProduto.qunatidade = 1

                return setCarrinho(carrinhoAnterior => [...CarrinhoAnterior, novoProduto])
            }

            setCarrinho(carrinhoAnterior => carrinhoAnterior.map(itemCarrinho => {
                if (itemCarrinho.id === novoProduto.id) itemCarrinho.qunatidade += 1
                return itemCarrinho
            }))
        }

        return (
            carrinho,
            setCarrinho,
            adicionarProduto
        )
    }

Esse hook utiliza do próprio contexto que já se encontra no arquivo, depois com a função some() procuramos se existe algum item do carrinho igual ao que recebemos, se tiver eu não quero adicionar outro objeto do mesmo item, eu só quero mudar a quantidade desse item e dessa forma no componente do produto:

    const {carinho , adicionarProduto} = useCarrinhoContext()

    const produtoNoCarrinho = carrinho.find(itemDoCarrinho => intemdoCarrinho.id === id)


    <ComponenteBotaoAdicionar
        onClick={() => adicionarProduto({nome, foto , id valor})}
    >
        {produtoNoCarrinho?.qunatidade || 0}
    <ComponenteBotaoAdicionar>

Chamamos a função adicionarProduto e passamosos parâmetro necessário e produtoNoCarrinho tenta procurar o id do produto no carrinho, caso ele ache ele coloca o valor certo da quantidade caso não ache apenas coloca um zero. Lembrando que a função find ela acah o produto e retorna ele para a constante.
