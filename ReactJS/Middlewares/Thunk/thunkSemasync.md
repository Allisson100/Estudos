# Thunk sem async

Criamos um novo addCase() no reducer de categorias.js:

    .addCase(
        resetarCarrinho.type,
        () => {
            toast({
                title: 'Sucesso!',
                description: 'Compra completada com sucesso!',
                status: 'success',
                duration: 2000,
                isClosable: true
            })
        }
    )

Como podemos ver aqui dentro do reducer de categorias estamos usando uma action do reducer de carrinho. E estamos somente aplicando uma função que gera um toast.

Nesse caso foi só um exemplo de que é possícel utilzar outras actions de outros reducer e isso pode servir caso nós precisarmos mudar alguma coisa aqui dentro do reducer de categorias quando alguma action do reducer do carrinho ou qualquer outro reducer for ativado.