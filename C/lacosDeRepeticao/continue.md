# Continue

Enquanto o break para a repetição, agora utilizamos o comaqndo continue;. Utilizamos ele, pois queremos que quando o usuário digitar um número negativo apareça uma mensagem dizendo que não pode colocar núemros negativos no jog e também não queremos que isso conte como uma tentativa e para isso fazemos o seguinte:

    if (chute < 0) {
        printf("Você não pode chutar números negativos!\n");
        i--;

        continue;
    }

Nosso código final está assim por enquanto:

    #include <stdio.h>

    #define NUMERO_DE_TENTATIVAS 5

    int main() {

        printf("******************************************\n");
        printf("* Bem vindo ao nosso jogo de adivinhação *\n");
        printf("******************************************\n");

        int numerosecreto = 42;
        int chute;

        for (int i = 1; i <= NUMERO_DE_TENTATIVAS; i++) {

            printf("Tentativa %d de %d\n", i, NUMERO_DE_TENTATIVAS);
            printf("Qual é o seu chute? ");

            scanf("%d", &chute);
            printf("Seu chute foi %d\n", chute);

            if (chute < 0) {
                printf("Você não pode chutar números negativos!\n");
                i--;

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
        }

        printf("Fim de Jogo!");
    }
