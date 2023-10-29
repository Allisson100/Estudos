# scanf() e printf()

Exemplo de um projeto que desenvolvi com esses exemplos:

Para conseguirmos obter um dado do usuário usamos a função scanf():

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
        printf("Seu chute foi %d", chute);
    }

Nós a utilizamos dessa maneira:

    scanf("%d", &chute);

o & iremos ver mais para frente no curso, mas basicamente temos que colocar entre "" a variável que iremos obter do usuário e depois a variável em que vamos guardar esse dado do usuario junto com o &.
