# Header files

Temos um problema que devemos colcoar as funções na ordem certa, pois por exemplo, não podemos charmar um função na linha 10 que só é criada na linha 50. Isso pode ser um grande problema na hora de programar, pois imagina se tiver muitas funções diferentes como que vamos organizar isso. Para resolver esse problema podemos criar uma assisnatura da função no começo do arquivo dessa forma:

    #include <stdio.h>
    #include <string.h>

    int enforcou();
    int acertou();
    void escolhepalavra();
    void desenhaforca();
    int jachutou(char letra);
    void chuta();
    void abertura();

    char palavrasecreta[20];
    char chutes[26];
    int chutesdados = 0;

    void abertura() {

        printf("*********************\n");
        printf("*   Jogo da Forca   *\n");
        printf("*********************\n\n");
    };

    void chuta() {

        char chute;
        scanf(" %c", &chute);

        chutes[chutesdados] = chute;
        chutesdados++;
    };

    int jachutou(char letra) {

        int achou = 0;

        for(int j = 0; j < chutesdados; j++) {
            if(chutes[j] == letra) {
                achou = 1;
                break;
            }
        }

        return achou;
    }

    void desenhaforca() {

        for (int i = 0; i < strlen(palavrasecreta); i++) {

            int achou = jachutou(palavrasecreta[i]);

            if (achou) {
                printf("%c ", palavrasecreta[i]);

            } else {
                printf("_ ");
            }

        }
        printf("\n");
    }

    void escolhepalavra() {
        sprintf(palavrasecreta, "MELANCIA");
    }

    int acertou() {
        for(int i = 0; i < strlen(palavrasecreta); i++) {

            if(!jachutou(palavrasecreta[i])) {
                return 0;
            }
        }

        return 1;
    }

    int enforcou() {

        int erros = 0;

        for(int i = 0; i < chutesdados; i++) {

            int existe = 0;

            for(int j = 0; j < strlen(palavrasecreta); j++) {

                if (chutes[i] == palavrasecreta[j]) {

                    existe = 1;
                    break;
                }
            }

            if(!existe) erros++;
        }

        return erros >= 5;
    }

    int main() {

        escolhepalavra();
        abertura();

        do {

            desenhaforca();

            chuta();

        } while(!acertou() && !enforcou());
    }

Porém para ficar mais organizado vamos criar um arquivo chamado forca.h, e nesse arquivo vamos colcoar nossas funções:

    int enforcou();
    int acertou();
    void escolhepalavra();
    void desenhaforca();
    int jachutou(char letra);
    void chuta();
    void abertura();

E para chamar esse arquivo no projeto principal forca.c digitamos:

    #include <stdio.h>
    #include <string.h>
    #include "forca.h"
