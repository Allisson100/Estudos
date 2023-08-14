# Utilizando styled components

    yarn add styled-components

Dentro do arquivo styles.js de um componente digitamos:

    import { styled } from "styled-components"

    export const OrderListContainer = styled.div `
        align-items: center;
        border-bottom: 1px solid #ffffff;
        border-left: 1px solid #ffffff;
        border-right: 1px solid #ffffff;
        display: grid;
        grid-template-columns: 3fr 1fr 1fr 1fr;
        grid-template-rows: 1fr;
        height: 20%;
        justify-items: center;
        width: 100%;
    `

E no arquivo principal desse componente digitamos:

    import { OrderListContainer, OrderText, TrashIcon } from "./styles";
    import trashIcon from "../../assets/img/trashIcon.png";

    function OrderList({ order, deleteOrder }) {

        function handleDeleteOrder() {
            deleteOrder(order.id);
        }

        return (
            <OrderListContainer>
            <OrderText>{order.descricao}</OrderText>
            <OrderText>{order.qtd}</OrderText>
            <OrderText>{order.valor}</OrderText>
            <OrderText>
                <TrashIcon
                src={trashIcon}
                alt="trash icon"
                onClick={handleDeleteOrder}
                />
            </OrderText>
            </OrderListContainer>
        );
    }

    export default OrderList;
