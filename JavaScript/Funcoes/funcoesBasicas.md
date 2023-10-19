# Funções básicas do JavaScript

### Converter um tipo em string

    const numero = 256
    const convertidoEmString = new String(numero)

ou

    const num = 500
    console.log(num.toString()) //'500'

### Métodos para strings

### .length

    const palavra="alura";
    console.log(palavra.length) //5

### charAt()

Com o método charAt() conseguimos acessar um caractere de uma string. Lembre-se que, por baixo dos panos, strings são arrays de caracteres, e em cada posição temos o caractere que compõe a string.

    console.log("alura".charAt(3)) //r

Outra alternativa será usar a notação de colchetes para encontrar um caractere da string, da seguinte forma:

    const palavra="Alura"
    console.log(palavra[0]) //A

### indexOf()

Respondendo a pergunta anterior, existe a função indexOf(), que retorna a posição de um caractere dentro da string.

    const palavra="Alura"
    console.log(palavra.indexOf("a")) //4

O resultado é a posição 4. Porém, na utilização do indexOf(), fique atento caso o caractere que se busca na string seja encontrado em mais de uma posição, pois será retornada somente a primeira ocorrência.

    const palavra="Divertidamente"
    console.log(palavra.indexOf("e")) //3

### toUpperCase() e toLowerCase()

São duas funções bastante utilizadas quando estamos trabalhando com string e precisamos deixar o texto todo em letras minúsculas (lower case) ou todo em maiúsculas (upper case).

    const palavra="alura";
    console.log(palavra.toUpperCase()) //ALURA
    console.log(palavra.toLowerCase()) //alura

### substr()

Outra função muito interessante é a substr() (substring), que permite que façamos a extração de parte de uma string.

    let frase= "Mergulhando em tecnologia."
    console.log(frase.substr(0,11)) // Mergulhando

### slice()

Podemos utilizar também o método slice(), que usamos com arrays. Ele é similar ao substring() e retornará parte de uma string, desde que passemos nos parâmetros o índice de início e de fim.

    let frase= "Mergulhando em tecnologia."
    console.log(frase.slice(0,11)) // Mergulhando

### replace()

Com a função replace() temos a possibilidade de substituir parte de uma string por outra. Essa função recebe como parâmetros duas informações: a string que você quer substituir e a string que será colocada no lugar.

    let nome = "André";
    let comunicacao = " Olá, sr. nomeusurario, informamos que a partir da presente data o senhor tem 50% de desconto em nossa loja.";
    console.log(comunicacao.replace("nomeusurario",nome));

### concat()

O método concat() é uma opção para concatenar strings sem a utilização do operador de adição (+). Ele concatena duas strings, adicionando a nova string ao fim da anterior.

    let novaString = "Programe nas principais linguagens e plataformas. Explore linguagens como ";
    console.log(novaString.concat("JavaScript,").concat(" Python,").concat(" e C#."))

O resultado obtido será: Programe nas principais linguagens e plataformas. Explore linguagens como [JavaScript](https://www.alura.com.br/artigos/javascript), [Python](https://www.alura.com.br/artigos/python), e C#.

### split()

O método split() é bem interessante, pois com ele conseguimos quebrar uma string com base em caracteres separadores que vamos informar para o método como parâmetro.

    let linguagens = "JavaScript;Java;C#;PHP;Python;Go;Vb;SQL;C;C++";
    let arrayLinguagens = linguagens.split(";");
    console.log(arrayLinguagens)

Quando trabalhamos com o split(), devemos nos atentar, pois a execução gerará como resultado um array de strings com os elementos que foram separados com base no separador desejado. Portanto a execução do código resulta em um array.

    [ 'JavaScript',
    'Java',
    'C#',
    'PHP',
    'Python',
    'Go',
    'Vb',
    'SQL',
    'C',
    'C++' ]

### trim()

O trim() remove os espaços em branco no início ou fim de uma string. Se em alguma situação precisarmos fazer uma verificação de que o usuário não digitou o login com espaços.

    let login = "   andre@emailteste.com      ";
    let loginSemEspaco = login.trim();
    console.log(loginSemEspaco); //andre@emailteste.com

A variável loginSemEspaco conterá uma nova string, sem os espaços em branco no início ou fim que podem ter sido digitados.
No JavaScript ainda temos algumas variações desta função como: trimEnd(),trimStart(),trimLeft() e trimRight().
