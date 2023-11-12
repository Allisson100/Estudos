# Expressões regulares

Tesmo um site que se chama regex101 que nos juda a testar as expressões regulares que estamos criando.

Tipos de pesquisa:

- abc -> A expressão regular vai buscar no texto a sequencia de caracteres abc.
- [abc] -> A expressão regular vai buscar algora ocorrencias da letra a, letra b e letra c. Os [] são classes.
- [^abc] -> Pega todas a ocorrencias de letras menos a abc. A ^ faz essa negação para gente.
- [A-z] -> Dessa forma pega todas as ocorrencia de A até Z e a até z, porém não pega com acento.
- [^A-z] -> Dessa fomra ele pega tudo que não seja A até Z e a até z. Carcteres epeciais letras com acento etc.
- [\s] -> Pega todos os espaços em branco do texto.
- [\ss] -> Dessa forma ele pega todos os espaços em branco e todos os s.
- \[ -> assim ele pega todos os colchete que estão abrindo.
- [\[\]] -> Dessa fomra ele busca todos os colchetes abrindo e todos os que estão fechando.
- \[[\w]Asterisco?\] -> Dessa forma ele busca todos os texto que estão entre colchetes. (Coloquei a palavra asterico de vez \*, pois quando eu salvo ele colocar uma barra invertida antes do asterisco automaticamente.). Nesse caso ele só vai pagar as palavras entre colchetes e não vai pegar caratres especiais e nem duas palavras sepaadas por espaço em branco.
- \[[^[\]]asterisco?\] -> Dessa forma ele pega tudo que tem entre parenteses.

Dessa forma a gente já consegue pegar os itens entre colchetes, agora só falta pegar os links que sao os textos entre () que vem logo após de um texto entre[].

# Classes e grupos

Fizemos a seguinte expressão para obter os links que estão entre parenteses:

    \(https?:\/\/[^\s?#.].[^\s]*\)

Agora temos que juntar as duas expressõe sregulares que criamos.

# Capturando grupos

Temos como expressão final:

    \[([^[\]]*?)\]\((https?:\/\/[^\s?#.].[^\s]*)\)

Função:

    function extraiLinks (texto) {
        const regex = /\[([^[\]]*?)\]\((https?:\/\/[^\s?#.].[^\s]*)\)/gm;
        const capturas = texto.match(regex)
        console.log(capturas);
    }

Essa função faz com que a const capturas nos retorne um array com as ocorrencias encontradas atrvés do regex.

    function extraiLinks (texto) {
        const regex = /\[([^[\]]*?)\]\((https?:\/\/[^\s?#.].[^\s]*)\)/gm;
        const capturas = regex.exec(texto)
        console.log(capturas);
    }

Agora a mesma função porém utilizando regex nos retorna também os grupos, mas ele só retorna a primeira ocorrencia que ele e queremos todas. Vamos ver na próxima aula como fazer isso.

# Retornando os links

Para resolver o problema de receber apenas uma ocorrencia se resolve basicamente criando um Loop ou utilizando o spread operator:

    function extraiLinks (texto) {
        const regex = /\[([^[\]]*?)\]\((https?:\/\/[^\s?#.].[^\s]*)\)/gm;
        const capturas = [...texto.matchAll(regex)]
        const resultados = capturas.map((captura) => (
            {[captura[1]]: captura[2]}
        ))
        console.log(resultados);
    }

Temos a seguinte resultado:

    [
        {
        FileList: 'https://developer.mozilla.org/pt-BR/docs/Web/API/FileList'
        },
        {
        '<input>': 'https://developer.mozilla.org/pt-BR/docs/Web/HTML/Element/Input'
        },
        {
        DataTransfer: 'https://developer.mozilla.org/pt-BR/docs/Web/API/DataTransfer'
        },
        {
        HTMLCanvasElement: 'https://developer.mozilla.org/pt-BR/docs/Web/API/HTMLCanvasElement'
        },
        {
        'Implementation notes': 'https://developer.mozilla.org/pt-BR/docs/Web/API/File#implementation_notes'
        }
    ]

E vamos juntar tudo agora:

    import fs from 'fs';
    import chalk from 'chalk';

    function extraiLinks (texto) {
        const regex = /\[([^[\]]*?)\]\((https?:\/\/[^\s?#.].[^\s]*)\)/gm;
        const capturas = [...texto.matchAll(regex)]
        const resultados = capturas.map((captura) => ({[captura[1]]: captura[2]}))
        console.log(resultados);
    }

    function trataErro(erro) {
        throw new Error(chalk.red(erro.code, 'não há arquivo no diretório'));
    }

    async function pegaArquivo(caminhoDoArquivo) {

        try {
            const encoding = 'utf-8';

            const texto = await fs.promises.readFile(caminhoDoArquivo, encoding)
            extraiLinks(texto)
        } catch (erro) {
            trataErro(erro)
        }
    }

    pegaArquivo('./arquivos/texto.md')

Vale ressaltar que essa forma de escrever objetos {[captura[1]]: captura[2]} é feita desse jeito para termos esse resultados:

    [
        {
        FileList: 'https://developer.mozilla.org/pt-BR/docs/Web/API/FileList'
        },
        {
        '<input>': 'https://developer.mozilla.org/pt-BR/docs/Web/HTML/Element/Input'
        },
        {
        DataTransfer: 'https://developer.mozilla.org/pt-BR/docs/Web/API/DataTransfer'
        },
        {
        HTMLCanvasElement: 'https://developer.mozilla.org/pt-BR/docs/Web/API/HTMLCanvasElement'
        },
        {
        'Implementation notes': 'https://developer.mozilla.org/pt-BR/docs/Web/API/File#implementation_notes'
        },
        { 'Teste de retorno 400': 'https://httpstat.us/404' },
        { 'gatinho salsicha': 'http://gatinhosalsicha.com.br/' }
    ]

Como podem ver alguns captura[1] são strings e outros não e é por isso que escrever dessa forma com mais um colchete [captura[1]].
