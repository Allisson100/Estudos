# Outras diretivas de compilação

Aprendemos o que é diretrizes de compilação.

    #ifndef _UI_H_
    #define _UI_H_

    #include "mapa.h"

    void imprimemapa (MAPA* m);
    void imprimeparte(char desenho[4][7], int parte);

    #endif

Basicamente é usar essa estrutura de #ifndef e #endif em uma constante que nesse caso foi a #define _UI_H_.
