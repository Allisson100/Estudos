# Funções básicas

Vou adicionar aqui outras funções básicas porém com outros exemplos.

### .push()

Exemplo:

    const notas = [10, 6, 8];

    notas.push(7); // [10, 6, 8, 7]

### .pop()

Exemplo:

const notas = [10, 6, 8, 5.5, 10]

notas.pop(); // [10, 6, 8, 5.5]

### .slice()

const array = [20_nome_diferentes];

    const novoArray = array.slice(0,10)

Dessa forma o array será fatiado do item 0 até o 9, pois o 10 é o item final que não será incluído. E ele será armazenado na const novoArray

    const novoArrayDois = array.slice(10)

E dessa forma a const novoArrayDois receb o restante dos itens. Como passamos só um parâmetro, ele entende que queremos pegar do item 10 até o final e isso inclui o item 10.

### .splice()

const nomes = ['João', 'Ana', 'Caio', 'Lara', 'Majorie', 'Leo']

    nomes.splice(1, 2)

Dessa forma ele altera o array original e passamos como parâmetro (1 ,2) o que significa que vamos remover a partir do item 1 dois elementos, então nesse caso essa função vai remover a 'Ana' e o 'Caio' do array.

    nomes.splice(1, 2, 'Rodrigo')

Dessa forma ele vai continuar removendo os itens, porém vai adicionar o rodrigo no lugar deles. Isso é útil quando queremos remover alguns itens e adicionar outros, porém só será util se o item que será adicionado naõ afetar o código independente da posição dele no array.

O splice também é útil quando queremos colocar um item em uma posição específica, exemplo:

    nomes.splice(1 ,0, "outro nome")

Dessa forma ele vai colocar o novo nome na posição um do array e não irá remover nenhum item.

# .concat()

const salaJs = ['nome01', 'nome02', 'nome03']
const salaPhyton = ['nome04', 'nome05', 'nome06']

    const salasUnificadas = salaJs.concat(salaPhyton)

Dessa forma temos um novo array que é a união de todos os arrays.

# Lista com 2 dimensões

const alunos = ['João', 'Juliana', 'Ana', 'Caio']
const medias = ['10', '8', '7.5', '9']

const ListaDeAlunosEMedias = [alunos , medias]
// [['João', 'Juliana', 'Ana', 'Caio'], ['10', '8', '7.5', '9']]

Basicammente fica dois subarrays dentro de um array.

### .includes() e .indexof()

const alunos = ['João', 'Juliana', 'Ana', 'Caio']
const medias = ['10', '8', '7.5', '9']

    const listaDeAlunosEMedias = [alunos , medias]

    function exibeNomeENota(aluno) {
        if(listaDeAlunosEMedias[0].includes(aluno)) {
            console.log('Está cadastrado')

            const indice = listaDeAlunosEMedias[0].indexof(aluno)

            const nota = listaDeAlunosEMedias[1].[indice]

            console.log(nota)

        } else {
            console.log('Não está cadastrado')
        }
    }

    exibeNomeENota("João")

Dessa forma verificamos se o nome do aluno está cadastrado na lista.
Com o indeof eu tenho qual é a posição do aluno no array caso ele seja cadastrado e com isso eu consigo buscar qual é a nota dele.

### Desestruturando uma lista

    function exibeNomeENota(aluno) {
        if(listaDeAlunosEMedias[0].includes(aluno)) {

            // const alunos = listaDeAlunosEMedias[0]
            // const medias = listaDeAlunosEMedias[1]

            const [alunos , medias] = listaDeAlunosEMedias

            const indice = alunos.indexof(aluno)

            const nota = medias.[indice]

            console.log(nota)

        } else {
            console.log('Não está cadastrado')
        }
    }

Dessa forma conseguimos desestruturar um array, lembrando que no caso do array o que importa é a posição e não o nome. Já se a gnte quiser desestruturar um objeto, o que importa é o nome e não a posição.

### For clássico

const numeros = [100, 200, 300, 400, 500, 600]

    for(let i = 0; i < numeros.length; i++) {
        console.log(numeros[i])
    }

Ensina o loop.

### Média com for

Calculou a média de um array com o for.

### Média com for of

const notas = [10, 6.5, 8, 7.5]

    let somaDasNotas = 0;

    for (let nota of notas) {
        somaDasNotas += nota
    }

    const media = somaDasNotas / notas.length

    console.log(media)

Calculando a média com o for of

### .forEach()

const notas = [10, 6.5, 8, 7.5]

    let somaDasNotas = 0;

    notas.forEach((nota, indice) = > {
        somaDasNotas += nota
        console.log(indice)
    })

    const media = somaDasNotas / notas.length

    console.log(media)

Calculando média com forEach. E esse método nos retorna doisvalores tanto o item quanto a posição desse item que no caso é o indice.

### Revisando callbacks

Uma outra forma de passar utilizar o callback é:

    const nomes = ["Evaldo", "Mari", "Camis"]

    fuction imprimeNome(nome) {
    console.log(nome)
    }

    nome.forEach(imprimeNome)

### .map()

const notas = [10, 9.5, 8, 7, 6]

    const novasNotas = notas.map((nota) => {
        return nota + 1 >= 10 ? 10 : nota + 1
    })

Nesse caso ele modifica o array original retornando um novo array com as modificações.

### Alterando strings com .map()

const nomes = ['ana Julia', 'Caio vinicius','BIA sila']

    const nomesPadronizados = nomes.map((nome) => nome.toUpperCase())

### .filter()

const alunos = ['Ana', 'Marcos', 'Maria', 'Mauro']
const medias = ['7', '4.5', '8', '7.5']

    const reprovados = alunos.filter((aluno, indice) => {
        return medias[indice] < 7
    })

Como nesse caso não estamos usando o parâmetro aluno, podemos usar a seguinte formatação:

    const reprovados = alunos.filter((_, indice) => {
        return medias[indice] < 7
    })

Apenas trocamos alunos por underline.

### .reduce()

const salaJS = [7, 8, 8, 7, 10, 6.5, 4, 10, 7]
const salaJava = [6, 5, 8, 9, 5, 6]
const salaPython = [7, 3.5, 8, 9.5]

    function calculaMedia(notasDaSala) {
        const somaDasNotas = notasDaSala.reduce((acc, nota) => {
            return acc + nota
        }, 0)

        const media = somaDasNotas / notasDaSala.length

        return media
    }

Esse é um método bem comum para somar valores de um array.

### Clonando com spread operator

const notas = [7, 7, 8, 9]

    const novasNotas = [... notas, 10]

Ensinando a fazer uma cópia de um array.

### Removendo elementos repetidos

const nomes = ["Ana", "Clara", "Maria", "Maria", "João", "João", "João"]

    const meuSet = new Set(nomes)

    const tranformaObjetoDoNewSetEmAray = [... meuSet]

Dessa forma ele retorna um objeto, porém com os nomes sem estarem repetidos.

Podemos escrever assim também:

    const tranformaObjetoDoNewSetEmAray = [... new Set(nomes)]
