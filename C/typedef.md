# A instrução typedef

Essa intrução nos possibilita criar apelidos para a nossa struct:

    struct mapa {
        char** matriz;
        int linhas;
        int colunas;
    };

    typedef struct mapa MAPA;

E no nosso código fica assim:

    #include <stdio.h>
    #include <stdlib.h>
    #include "fogefoge.h"

    MAPA m;
