# abs()

Utilizamos uma função para sempre pegar valores positivos:

    double pontosperdidos = abs(chute - numerosecreto) / (double)2;
    pontos = pontos - pontosperdidos;

No nosso jogo a gente estava tendo um problema onde caso o resultado da conta chute - numerosecreto fosse negativo ele não iria subtrair dos pontos e sim somar, pois menos com menos vira mais, então essa nova função nos ajudar com isso, sempre deixa o valor positivo.

Lembrando que devemmos incluir uma nova biblioteca para utilizá-lo:

    #include <stdlib.h>
