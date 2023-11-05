# Escrevendo em um arquivo

Criamos a seguinte função para modificar nosso arquivo txt, pois a idea e permitir que usuário possa acrescentar palavras caso ele queira no final do jogo.

    void adicionapalavra() {

        char quer;

        printf("Voce deseja adicionar alguma nova palavra no jogo? (S/N)");
        scanf(" %c", &quer);

        if(quer == 'S') {

            char novapalavra[20];
            printf("Qual a nova palavra?");
            scanf("%s", novapalavra);

            FILE* f;

            f = fopen("palavras.txt", "r+");

            if(f == 0) {
                printf("Desculpe, banco de dados não disponivel!\n\n");
                exit(1);
            }

            int qtd;
            fscanf(f, "%d", &qtd);
            qtd++;

            fseek(f, 0, SEEK_SET);
            fprintf(f, "%d", qtd);

            fseek(f, 0, SEEK_END);
            fprintf(f, "\n%s", novapalavra);

            fclose(f);
        }
    }

A parte do código que não sabemos ainda é:

    int qtd;
    fscanf(f, "%d", &qtd);
    qtd++;

    fseek(f, 0, SEEK_SET);
    fprintf(f, "%d", qtd);

    fseek(f, 0, SEEK_END);
    fprintf(f, "\n%s", novapalavra);

    fclose(f);

Basicamente pegamos a quantidade itens lá do arquivo txt com fscanf(f, "%d", &qtd); depois apontar o ponteiro do arquivo na primeira linha e subescrever o valor que está lá para o novo, pois se vamos adicionar uma nova palavra entao teremos um valor a mais lá na primeira linha. Utilizamos esse comando para fazer isso:

    fseek(f, 0, SEEK_SET);
    fprintf(f, "%d", qtd);

E depois esse comando:

    fseek(f, 0, SEEK_END);
    fprintf(f, "\n%s", novapalavra);

Para apontar o ponteiro para o fnal do arquivo e acrescentarmos a nova palavra. Colocamos um \n ali, pois o último item não tem enter e é necessário para nosso programa funcionar direito.

E é claro após fazer as alterações desejadas no arquivo precismos fechá-lo com fclose(f);
