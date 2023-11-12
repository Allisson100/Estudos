# Ponteiros para structs

Aprendemos como separar o código em arquivos diferentes e como fazer ponterios de structs.

Criamos dois novos arquivos o mapa.c e o mapa.h nde vão ficar as funções do mapa.

mapa.c:

    #include <stdio.h>
    #include <stdlib.h>
    #include "mapa.h"

    void liberamapa(MAPA* m) {
        for (int i = 0; i < m->linhas; i++) {
            free(m->matriz[i]);
        }

        free(m->matriz);
    }

    void alocamapa(MAPA* m) {
        m->matriz = malloc(sizeof(char*) * m->linhas);
        for(int i = 0; i < m->linhas; i++) {
            m->matriz[i] = malloc(sizeof(char) * (m->colunas + 1));
        }
    }

    void lemapa(MAPA* m) {
        FILE* f;
        f = fopen("mapa.txt", "r");

        if(f == 0) {
            printf("Erro na leitura do mapa\n");
            exit(1);
        }

        fscanf(f, "%d %d", &(m->linhas), &(m->colunas));

        alocamapa(m);

        for (int i = 0; i < 5; i++) {
            fscanf(f, "%s", m->matriz[i]);
        }

        fclose(f);
    }

    void imprimemapa (MAPA* m) {
        for(int i = 0; i < 5; i++) {
            printf("%s\n", m->matriz[i]);
        }
    }

mapa.h:

    struct mapa {
        char** matriz;
        int linhas;
        int colunas;
    };

    typedef struct mapa MAPA;

    void liberamapa(MAPA* m);
    void lemapa(MAPA* m);
    void alocamapa(MAPA* m);
    void imprimemapa (MAPA* m);

E os arquivos que a gente já tinha ficaram dessa forma.

fogefoge.c:

    #include <stdio.h>
    #include <stdlib.h>
    #include "fogefoge.h"
    #include "mapa.h"

    MAPA m;

    int acabou () {
        return 0;
    }

    void move (char direcao) {
        int x;
        int y;

        for(int i = 0; i < m.linhas; i++) {
            for(int j = 0; j < m.colunas; j++) {
                if(m.matriz[i][j] == '@') {
                    x = i;
                    y = j;
                    break;
                }
            }
        }

        switch(direcao) {
            case 'a':
                m.matriz[x][y-1] = '@';
                break;

            case 'w':
                m.matriz[x-1][y] = '@';
                break;

            case 's':
                m.matriz[x+1][y] = '@';
                break;

            case 'd':
                m.matriz[x][y+1] = '@';
                break;
        }

        m.matriz[x][y] = '.';

    }

    int main () {

    lemapa(&m);

        do {

            imprimemapa(&m);

            char comando;
            scanf(" %c", &comando);
            move(comando);

        } while (!acabou());


        liberamapa(&m);
    }

fogefoge.h:

    void move (char direcao);
    int acabou ();

Mas agora nós temos que compilar os dois arquivos .c juntos, então no terminal fica da seguinte forma:

    gcc fogefoge.c mapa.c -o fogefoge.exe

E vimos também que para acessar o conteúdo de uma struct podemos utilziar a seguinte sintaxe:

    m->linhas

Que nem essa função:

    void liberamapa(MAPA* m) {
        for (int i = 0; i < m->linhas; i++) {
            free(m->matriz[i]);
        }

        free(m->matriz);
    }

Antes a gente utilizava:

    (*m).linhas
