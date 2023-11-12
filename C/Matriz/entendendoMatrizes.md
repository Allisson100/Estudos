# Entendendo as matrizes

Definimos primeiro o mapa do jogo:

|--------|
|...|..-.|
|..-|.@..|
|......-.|
|--------|

E depois criamos nossa primeira matriz, pois é dessa forma que vamos criar o mapa:

    #include <stdio.h>

    int main () {
        // matriz de 5 x 10
        char mapa[5][10];

        mapa [0][0] = '|';
        mapa [4][9] = '@';

        printf("%c %c", mapa[0][0], mapa[4][9]);
        //saída: | @
    }

# Salvando e lendo dados de uma matriz

Nós vamos ler o nosso arquivo mapa.txt que é onde se encontra o mapa e depois imprimi-lo na tela:

    #include <stdio.h>
    #include <stdlib.h>

    int main () {
        // matriz de 5 x 10
        char mapa[5][10+1];

        FILE* f;
        f = fopen("mapa.txt", "r");

        if(f == 0) {
            printf("Erro na leitura do mapa\n");
            exit(1);
        }

        for (int i = 0; i < 5; i++) {
            fscanf(f, "%s", mapa[i]);
        }

        for(int i = 0; i < 5; i++) {
            printf("%s\n", mapa[i]);
        }

        fclose(f);
    }

Primeiro definimos a matriz e depois abrimos o arquivo do mapa e depois interamos cada linha do arquivo em cada linha da matriz.

Utilizamos fscanf(f, "%s", mapa[i]); apenas com um abre e fecha colchetes, pois dessa forma ele vai lendo linha a linha do arquivo e salvando linha a linha da matriz, mas poderiamos também utilizar dois abre e fecha colchetes para deixar específico uma posição na matriz.

E depois atrvés do looping imprimos cada posição da matriz na tela, também utilizando apenas um abre e fecha colchetes.

Lembrando que o char mapa[5][10+1]; 10 + 1 é por conta do /0 que tem no final do array para o computador saber qual é o fim do array.
