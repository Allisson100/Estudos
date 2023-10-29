# while

Nesse exemplo utilizamos o while, que no caso utilizamos 1, mas poderiamos utilizar uma condição verdadeira nele para que o loop continue e no nosso caso a gente da um break ou um continue para quebrar o looping de acordo com as condições.

#include <stdio.h>

    int main() {

        printf("******************************************\n");
        printf("* Bem vindo ao nosso jogo de adivinhação *\n");
        printf("******************************************\n");

        int numerosecreto = 42;
        int chute;
        int tentativas = 1;

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
        }

        printf("Fim de Jogo!\n");
        printf("Você certou em %d tentativas", tentativas);
    }
