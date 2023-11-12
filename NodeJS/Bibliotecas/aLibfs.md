# A lib fs

Vamos utilizar agora a biblioteca fs, pois ela consegue ler arquivos de fora que não sejam .js.

Não precisamos instalar essa biblioteca com npm, pois ela já é uma biblioteca nativa do NodeJS.

No nosso arquivo index.js dgitamos:

    import fs from 'fs';
    import chalk from 'chalk';

    function pegaArquivo(caminhoDoArquivo) {
        const encoding = 'utf-8'
        fs.readFile(caminhoDoArquivo, encoding, (erro, texto) => {
            console.log(chalk.green(texto));
        })
    }

    pegaArquivo('./arquivos/texto.md')

Importamos a biblioteca fs. Para utilizá-la devemos passar os parâmetros como o caminho do arquivo e esse caminha é com base na past em que está o arquivo index.js no momento. Depois passamos o encodign que é o padrão de escrita, no nosso caso o utf-8, e também chamamos uma função callback e nessa função temos dois parâmetros que são o erro e o retorno, como nesse caso estamos lendo um arquivo markdown esperamos que nos retorne um texto, então por isso colocamos o nome de texto.

# Promessas

Refatoramos a função para trabalhar de forma assincrona, pois não sabemos qual é o tamanho dos arquivos que vamos receber e se deixarmos o código sincrono pode dar algum problema. Vamos começar usando o .then() e .catch():

    import fs from 'fs';
    import chalk from 'chalk';

    function trataErro(erro) {
        throw new Error(chalk.red(erro.code, 'não há arquivo no diretório'));
    }

    function pegaArquivo(caminhoDoArquivo) {

        const encoding = 'utf-8';

        fs.promises.readFile(caminhoDoArquivo, encoding)
            .then((texto) => console.log(chalk.green(texto)))
            .catch(trataErro)
    }

Como a função .catch() recebe uma função callback como parâmetro podemos simplesmente fazer dessa forma:

    .catch(trataErro)

Pois de baixo dos panos a função catch() está passando o parâmetro erro para a função trataErro.

O .then() também recebe uma função callback, mas através do parâmetro pegamos o return que no nosso caso e o texto e tratamos ele da forma que charmos melhor.

# async/await

Refatoramos a função para continaur assincrona, mas usando o try catch e async await:

    import fs from 'fs';
    import chalk from 'chalk';

    function trataErro(erro) {
        throw new Error(chalk.red(erro.code, 'não há arquivo no diretório'));
    }

    async function pegaArquivo(caminhoDoArquivo) {

        try {
            const encoding = 'utf-8';

            const texto = await fs.promises.readFile(caminhoDoArquivo, encoding)
            console.log(chalk.blue(texto));
        } catch (erro) {
            trataErro(erro)
        }
    }

    pegaArquivo('./arquivos/texto.md')
