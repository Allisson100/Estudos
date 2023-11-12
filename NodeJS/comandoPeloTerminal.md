# Executando comandos

Vamos agora criar um sistema onde pelo terminal eu consigo passar o caminho do meu arquivo.md e não deixe mais ele de forma estático lá na função.

Para isso vamos criar uma pasta chamada src na raiz do projeto e vamos colocar o arquivo index.js dentro dele.

dentro da pasta vamos criar também um arquivo chamado cli.js e nele digitamos:

    const caminho = process.argv;
    console.log(caminho);

Se rodarmos esse arquivo no terminal teremos:

    [
        'C:\\Program Files\\nodejs\\node.exe',
        'C:\\Users\\Francisco\\Desktop\\Github\\CursosEmAndamento\\NodeJS-Criando-SuaPrimeira-Biblioteca\\src\\cli.js'
    ]

Temos dois caminho absoluto em string, ou seja, ele nos retornou o que acontece por debaixo dos panos. O comando node acessar quele caminho e o comando src/csli.js percorre aquele caminho.

Quando digitamos no terminal:

    node src/cli.js oi

Ele nos retorna:

    [
        'C:\\Program Files\\nodejs\\node.exe',
        'C:\\Users\\Francisco\\Desktop\\Github\\CursosEmAndamento\\NodeJS-Criando-SuaPrimeira-Biblioteca\\src\\cli.js',
        'oi'
    ]

No arquivo index.js exportamos a função pegarArquivo para utilizá-la no arquivo cli.js:

    import pegaArquivo from "./index.js";

    const caminho = process.argv;

    pegaArquivo(caminho[2])
    console.log(caminho);

# Processando diretórios

Agora queremos passar para o terminal uma pasta e que o nosso programa acesse essa pasta e verifique os links de todos os arquivos presentes nela.

No arquivo cli.js criamos:

    async function processaTexto(argumentos) {
        const caminho = argumentos[2];

        if (fs.lstatSync(caminho).isFile()) {
            const resultado = await pegaArquivo(caminho)
            console.log(chalk.yellow('lista de links'), resultado);
        } else if (fs.lstatSync(caminho).isDirectory()) {
            const arquivos = await fs.promises.readdir(caminho)
            console.log(arquivos);
        }
    }

    processaTexto(caminho)

Utilizamos metodos da biblioteca fs para podermos saber se o caminho que estamos passando no terminal é um diretório ou é um caminho direto de um arquivo e utilizamos o if para fazer essas verificações.

O console.log(arquivos); quando colocamos no terminal node src/cli.js arquivos\ nos retorna:

    [ 'texto.md' ]

Que é realmente os arquivos presentes dentro da pasta arquivos.

E finalizamos o código nessa aula da seguinte forma:

    import chalk from "chalk";
    import fs from 'fs'
    import pegaArquivo from "./index.js";

    const caminho = process.argv;

    function imprimeLista(resultado) {
        console.log(chalk.yellow("Lista de links"), resultado);
    }

    async function processaTexto(argumentos) {
        const caminho = argumentos[2];

        if (fs.lstatSync(caminho).isFile()) {
            const resultado = await pegaArquivo(caminho)
            imprimeLista(resultado)
        } else if (fs.lstatSync(caminho).isDirectory()) {
            const arquivos = await fs.promises.readdir(caminho)
            arquivos.forEach(async (nomeDeArquivo) => {
                const lista = await pegaArquivo(`${caminho}/${nomeDeArquivo}`)
                imprimeLista(lista)
            })
        }
    }

    processaTexto(caminho)

# Tratando novos erros

Criamos um trata,ento de erro para caso o usuário digite errado o caminho do diretorio ou do arquivo.

    async function processaTexto(argumentos) {
        const caminho = argumentos[2];

        try {
            fs.lstatSync(caminho)
        } catch (erro) {
            if(erro.code === 'ENOENT') {
                console.log('arquivo ou diretório não existe');
                return;
            }
        }

        if (fs.lstatSync(caminho).isFile()) {
            const resultado = await pegaArquivo(caminho)
            imprimeLista(resultado)
        } else if (fs.lstatSync(caminho).isDirectory()) {
            const arquivos = await fs.promises.readdir(caminho)
            arquivos.forEach(async (nomeDeArquivo) => {
                const lista = await pegaArquivo(`${caminho}/${nomeDeArquivo}`)
                imprimeLista(lista)
            })
        }
    }

Primeiro criamos um bloco try catch para tentar fazer alguma coisa com esse caminho fs.lstatSync(caminho) e aqui já possivel dar um erro caso o o usuário tiver digitado errado e tratamos o erro no catch. Vale ressaltar que utilzamos a verificação através do código do erro e logo após o return mandamos colcamos um return, pois não queremos que o erro apareça para o usuário e sim somente a mensagem de erro que criamos.

Terminamos com o código assim no arquivo cli.js:

    import chalk from "chalk";
    import fs from 'fs'
    import pegaArquivo from "./index.js";

    const caminho = process.argv;

    function imprimeLista(resultado, identificador = "") {
        console.log(
            chalk.yellow("Lista de links"),
            chalk.black.bgGreen(identificador),
            resultado
        );
    }

    async function processaTexto(argumentos) {
        const caminho = argumentos[2];

        try {
            fs.lstatSync(caminho)
        } catch (erro) {
            if(erro.code === 'ENOENT') {
                console.log('arquivo ou diretório não existe');
                return;
            }
        }

        if (fs.lstatSync(caminho).isFile()) {
            const resultado = await pegaArquivo(caminho)
            imprimeLista(resultado)
        } else if (fs.lstatSync(caminho).isDirectory()) {
            const arquivos = await fs.promises.readdir(caminho)
            arquivos.forEach(async (nomeDeArquivo) => {
                const lista = await pegaArquivo(`${caminho}/${nomeDeArquivo}`)
                imprimeLista(lista, nomeDeArquivo)
            })
        }
    }

    processaTexto(caminho)
