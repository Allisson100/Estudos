# Lendo arquivos

Agora precisamos deixar aleatório as palavras, pois até o momento estamos apenas com a palavra MELANCIA para ser acertada.

Para fazer isso vamos criar um arquivo chamado palavras.txt e nele deigitamos as palavras que queremos, no nosso caso escrevemos:

    MELANCIA
    MORANGO
    MELAO

No nosso arquivo principal forca.c, na função escolhapalavra() digitamos:

    void escolhepalavra() {

        FILE* f;

        f = fopen("palavras.txt", "r");

        if(f == 0) {
            printf("Desculpe, banco de dados não disponivel!");
            exist(1);
        }

        int qtddepalavras;
        fscanf(f, "%d", &qtddepalavras);

        srand(time(0));
        int randomico = rand() % qtddepalavras;

        for(int i = 0; i <= randomico; i++) {
            fscanf(f, "%s", palavrasecreta);
        }

        fclose(f);
    }

Esse é um conceito novo que aprendemos que é ler arquivos txt e pegar seu conteúdo e utilizar em nosso código.

Nosso arquivo txt está assim:

    3
    MELANCIA
    MORANGO
    MELAO

Na primeira linha aderimos como padrão colocar a quantidade de palavras que existem no arquivo paa facilitar a leitura.

    FILE* f;

    f = fopen("palavras.txt", "r");

    if(f == 0) {
        printf("Desculpe, banco de dados não disponivel!");
        exit(1);
    }

A linha f = fopen("palavras.txt", "r"); é o que no retorna o arquivo, utilizamos a função fopen para abrir o arquivo e nele devemos passar dois parâmetros que são o nome do arquivos e o que queremos fazer com ele que no caso é ler o arquivo por isso colocamos a letra r de read e ambos os parâmetros tem que ser passados como strings.

Precisamos também definir essa variável e por isso colocamos FILE* f; e como o f nos retorna um ponteiro devemos utilizar o *.

O if serve apenas para aparecer uma mensagem e finalizar o programa caso não seja possivel ler o arquivo.

    int qtddepalavras;
    fscanf(f, "%d", &qtddepalavras);

    srand(time(0));
    int randomico = rand() % qtddepalavras;

    for(int i = 0; i <= randomico; i++) {
        fscanf(f, "%s", palavrasecreta);
    }

    fclose(f);

Depois temos o restante do código que primeiro defini uma variável int qtddepalavras; e utilizamos o fscanf para ler o a primeira linha do arquivo e nele também passamos parâmetros. Primeiro a variavel que contem o arquivo que no nosso caso é o f. Depois o que iremos ler na primeira linha que no nosso caso é um número, pois definimos esse padrão. E terceiro a referencia de memória da variável quie queremos guardar esse valor do arquivo.

Após isso definimos um número randomico que já aprendemos como funciona antes.

E basicamente criamos um loop para salvarmos cada palavra na variavel palavrasecreta.

Basicamente ele vai ficar salvando por cima as palavras até chegar na ultima interação do Loop por isso que esse for funciona bem para o nosso caso, pois irá guardar a última palavra lida na variável.

Vale ressaltar que conforme o arquivo está em execução o ponteiro que está lendo o arquivo nunca reseta, então o código fscanf(f, "%d", &qtddepalavras); leu a linha 0 desse arquivo e nesse comando fscanf(f, "%s", palavrasecreta); já começou na linha dois do arquivo.

E por fim todo arquivo que a gente abriu para ler devemos fechá-los e por isso usamos o fclose(f);
