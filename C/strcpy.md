# Usando estruturas auxiliares

Criamos uma estruturar auxiliar que no nosso caso foi a copia do mapa original, pois dessa forma sempre conseguimos ver como estava o mapa anteriormente e assim analisar como queremos o mapa futuramente para que possamos mover os fantasmas corretamente.

A função que copia o mapa original é:

    void copiamapa(MAPA* destino, MAPA* origem)  {
        destino->linhas = origem->linhas;
        destino->colunas = origem->colunas;

        alocamapa(destino);
        for(int i = 0; i < origem->linhas; i++) {
            strcpy(destino->matriz[i], origem->matriz[i]);
        }
    }

Utilizamos o função strcpy da lib #include <string.h> para que ela faça a cópia das strings no novo mapa e utilizamos a mesma função para alocar o mapa na memória.

E temos também a função fantasma:

    void fastasmas () {
        MAPA copia;

        copiamapa(&copia, &m);

        for(int i = 0; i < m.linhas; i++) {
            for(int j = 0; j < m.colunas; j++) {

                if(copia.matriz[i][j] == FANTASMA) {
                    if(ehvalida(&m, i, j+1) && ehvazia(&m, i, j+1)) {
                        andanomapa(&m, i, j, i, j+1);
                    }
                }
            }
        }

        liberamapa(&copia);
    }

Que é chamada logo após a função move():

    int main () {

    lemapa(&m);
    encontramapa(&m, &heroi, HEROI);

        do {

            imprimemapa(&m);

            char comando;
            scanf(" %c", &comando);
            move(comando);
            fastasmas();

        } while (!acabou());


        liberamapa(&m);
    }

A função fantasma() faz a cópia do mapa atual para ter a comparação, depois ele fz a varredura do mapa original e para cada fantasma encontrado ele vevrifica se a próxima posição que quewremos mover o fastama é valida, ou seja, se não é uma parede ou se não está nos extremos, caso ele possa se mover, o fantasma se move uma casa para a direita com a função que reutilizamos andanomapa().
