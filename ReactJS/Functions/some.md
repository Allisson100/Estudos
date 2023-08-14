# some()

Utilizamos a função .some() para verificar se existe algum item em um array, é semelhante ao .filter().

    if (itemCardapio.codigo === "chantily") {
        const coffee = orderList.some((order) => order.codigo === "cafe");

        if (!coffee) {
            alert("Item extra não pode ser pedido sem o principal");
            setInputValue("");
            return;
        }
    }

Nesse caso utilizamos para uma verificação.

A const cofee vai retornar um valor true ou false:

    const coffee = orderList.some((order) => order.codigo === "cafe");

Essa lógica verifica se existe algum código "cafe" dentro do array orderList e se não existir, ele não deixa dar continuidade ao código.
