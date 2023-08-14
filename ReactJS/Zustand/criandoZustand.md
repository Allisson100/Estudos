# Criando Zustand

Para criar uma variável global com Zustand temos que primeiro criar a estrutura, pasta store dentro da src e dentro da pasta store criar um arquivo chamado useEOTemaDaVariável.

Lembrando que temos que instalar ele com:

    yarn add zutand

Exemplos do projeto do desafio de criar uma interface para uma lanchonete:

Arquivo useCartStore.js:

    import { create } from "zustand"

    export const useCartStore = create((set) => ({
        cartItems: [],
        setCartItems: (newItem) => set(() => ({cartItems: newItem }))
    }))

Para usá-lo em outro arquivo basta importar o useCartStore e digitar:

    {cartItems , setCartItems} = useCartStore()

Podemos criar uma outra estrutura também:

    import { create } from "zustand"

    export const useCartStore = create((set) => ({
        cartItems: [],
        setCartItems: (newItem) => set(() => ({cartItems: [... state.cartItems, newItem] }))
    }))

Dessa forma criamos um array que sempre vamos crescentando itens nele.

Outro exemplo do mesmo desafio:

    import { create } from "zustand"

    export const useOrderList = create((set) => ({
        orderList: [],
        setOrderList: (newOrder) => set((state) => ({orderList: newOrder }))
    }))

Lembrando que podemos usar o persist com o zustand também que nada mais que um sistema de persistência de dados que vem junto com a biblioteca e fuciona semelhante ao localStorage.
