No nosso jogo que desenvolvemos temos um exemplo de switch case que utilizamos para acrescentar a funcionalidade de dificuldade do jogo.

# Acrescentando níveis de dificuldade

Acrescentamos outra funcionalidade em nosso jogo, adicionamos a dificuldade do jogo e fizemos isso com o swutch case.

    int nivel;
    printf("Qual o nível de dificuldade?\n");
    printf("(1) - Fácil\n(2) - Médio\n(3) - Difícil\n\n");
    printf("Escolha: ");
    scanf("%d", &nivel);

    int numerosdetentativas;

    switch(nivel) {
        case 1:
            numerosdetentativas = 20;
            break;

        case 2:
            numerosdetentativas = 10;
            break;

        default:
            numerosdetentativas = 5;
            break;
    }

O código final está assim por enquanto:

    #include <stdio.h>
    #include <stdlib.h>
    #include <time.h>

    int main() {

        printf("******************************************\n");
        printf("* Bem vindo ao nosso jogo de adivinhação *\n");
        printf("******************************************\n");

        int segundos = time(0);
        srand(segundos);

        int numerogrande = rand();
        int numerosecreto = numerogrande % 100;

        int chute;
        int tentativas = 1;
        double pontos = 1000;

        int acertou = 0;

        int nivel;
        printf("Qual o nível de dificuldade?\n");
        printf("(1) - Fácil\n(2) - Médio\n(3) - Difícil\n\n");
        printf("Escolha: ");
        scanf("%d", &nivel);

        int numerosdetentativas;

        switch(nivel) {
            case 1:
                numerosdetentativas = 20;
                break;

            case 2:
                numerosdetentativas = 10;
                break;

            default:
                numerosdetentativas = 5;
                break;
        }

        for(int i = 1; i <= numerosdetentativas; i++) {

            printf("Tentativa %d\n", tentativas);
            printf("Qual é o seu chute? ");

            scanf("%d", &chute);
            printf("Seu chute foi %d\n", chute);

            if (chute < 0) {
                printf("Você não pode chutar números negativos!\n");

                continue;
            }

            acertou = (chute == numerosecreto);
            int maior = chute > numerosecreto;
            int menor = chute < numerosecreto;

            if (acertou){
                break;

            } else if (maior) {
                printf("Seu chute foi maior que o número secreto!\n");

            } else {

                printf("Seu chute foi menor que o número secreto!\n");
            }

            tentativas++;

            double pontosperdidos = abs(chute - numerosecreto) / (double)2;
            pontos = pontos - pontosperdidos;
        }

        printf("Fim de Jogo!\n");

        if (acertou) {
            printf("Parabéns! Você ganhou!\n");
            printf("Você certou em %d tentativas\n", tentativas);
            printf("Total de pontos:  %.1f\n", pontos);

        } else {
            printf("Você perdeu, tente novamente!\n");
        }
    }
