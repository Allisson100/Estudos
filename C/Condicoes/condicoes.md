# Definindo condições

Para criarmos condições fazemos da seguinte forma:

#include <stdio.h>

    int main()
    {
        printf("******************************************\n");
        printf("* Bem vindo ao nosso jogo de adivinhação *\n");
        printf("******************************************\n");

        int numerosecreto = 42;

        printf("O número %d é o secreto!\n", numerosecreto);

        int chute;

        printf("Qual é o seu chute? ");
        scanf("%d", &chute);
        printf("Seu chute foi %d\n", chute);

        if (chute == numerosecreto)
        {
            printf("Parabéns! Você acertou!\n");
        }
        else
        {
            printf("Você errou!\n");
        }
    }

Estrutura padrão de um if else e devemos usar o ==.
