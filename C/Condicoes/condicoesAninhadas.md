# If e else

    Criamos condições aninhadas:

    int main()
    {
        printf("******************************************\n");
        printf("* Bem vindo ao nosso jogo de adivinhação *\n");
        printf("******************************************\n");

        int numerosecreto = 42;
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
            if (chute > numerosecreto)
            {
                printf("Seu chute foi maior que o número secreto!\n");
            }
            else
            {
                printf("Seu chute foi menor que o número secreto!\n");
            }

            printf("Você errou!\n");
        }
    }

Aqui usamos if e else, mas não impede de eu usar dois if ao invés de um if e um else.
