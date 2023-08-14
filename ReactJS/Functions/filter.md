# filter()

Como usar o filter para fazer uma pesquisa em tempo real em uma lista:

cardapio:

    const cardapio = [
        {
            id: Math.random(),
            codigo: 'cafe',
            descricao: 'Café',
            valor: 'R$ 3,00'
        },
        {
            id: Math.random(),
            codigo: 'chantily',
            descricao: 'Chantily (extra do Café)',
            valor: 'R$ 1,50'
        },
        {
            id: Math.random(),
            codigo: 'suco',
            descricao: 'Suco Natural',
            valor: 'R$ 6,20'
        },
        {
            id: Math.random(),
            codigo: 'sanduiche',
            descricao: 'Sanduíche',
            valor: 'R$ 6,50'
        },
        {
            id: Math.random(),
            codigo: 'queijo',
            descricao: 'Queijo (extra do Sanduíche)',
            valor: 'R$ 2,00'
        },
        {
            id: Math.random(),
            codigo: 'salgado',
            descricao: 'Salgado',
            valor: 'R$ 7,25'
        },
        {
            id: Math.random(),
            codigo: 'combo1',
            descricao: '1 Suco e 1 Sanduíche',
            valor: 'R$ 9,50'
        },
        {
            id: Math.random(),
            codigo: 'combo2',
            descricao: '1 Café e 1 Sanduíche',
            valor: 'R$ 7,50'
        },
        {
            id: Math.random(),
            codigo: '',
            descricao: 'Código Inválido',
            valor: 'R$ 7,50'
        }
    ]

    export default cardapio

Componente:

    {cardapio
        .filter((item) =>
            inputValue !== ""
            ? item.codigo.startsWith(inputValue.toLowerCase())
            : true
        )
        .map((itemCardapio) => (
            <MenuCard key={itemCardapio.id} itemCardapio={itemCardapio} />
        ))
    }

Fizemos o .map() de uma lista mas antes fizemos um filter para que o usuário conseguisse fazer uma busca caso precise, basicamente a lógica é a seguinte, caso inputValue seja vazio, ou seja, não está pesquisando nada, então todos os itens da lista recebe um valor true que por sua vez é feito na função .map().

Mas caso o valor do inputValue for diferente de vazio então ele aplica a lógica:

    item.codigo.startsWith(inputValue.toLowerCase())

Eu quero que ele pegue somente os códigos dos itens que começam com as letras que estão no inputValue, por isso o uso da função .startsWith() e também utilizamos o .toLowerCase() para sempre bucar com as letras minúsculas, pois os códigos na const cardápio estão em minúsculo também.
