# Trabalhando com casas decimais

Arrumamos nosso código para que ele funcione com o tipo double, pois quando utilizavamos inteiro o cálculo não era preciso, pois ele utilizava numeros inteiro e não decimais. Como o compilador le o código da direita para esquerda, falamos apra a expressão dividir os números por 2.0, pois assim o compilador já define que a variável será um double.

    #include <stdio.h>

    int main() {

        printf("******************************************\n");
        printf("* Bem vindo ao nosso jogo de adivinhação *\n");
        printf("******************************************\n");

        int numerosecreto = 42;

        int chute;
        int tentativas = 1;

        double pontos = 1000;

        while (1) {

            printf("Tentativa %d\n", tentativas);
            printf("Qual é o seu chute? ");

            scanf("%d", &chute);
            printf("Seu chute foi %d\n", chute);

            if (chute < 0) {
                printf("Você não pode chutar números negativos!\n");

                continue;
            }

            int acertou = (chute == numerosecreto);
            int maior = chute > numerosecreto;
            int menor = chute < numerosecreto;

            if (acertou){
                printf("Parabéns! Você acertou!\n");

                break;

            } else if (maior) {
                printf("Seu chute foi maior que o número secreto!\n");

            } else {

                printf("Seu chute foi menor que o número secreto!\n");
            }

            tentativas++;

            double pontosperdidos = (chute - numerosecreto) / 2.0;
            pontos = pontos - pontosperdidos;
        }

        printf("Fim de Jogo!\n");
        printf("Você certou em %d tentativas\n", tentativas);
        printf("Total de pontos:  %f\n", pontos);
    }

# Dica para uso do double

    printf("Total de pontos:  %.1f\n", pontos);

Mudamos apenas essa linha de código para limitar o número de casas decimais.
