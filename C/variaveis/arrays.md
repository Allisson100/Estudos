# Conhecendo os arrays

Vamos começar criando um projeto padrão em C:

    #include <stdio.h>

    int main() {

    }

Inserindo caracter:

    #include <stdio.h>

    int main() {
        char letra1 = 'M';
        char letra2 = 'E';
        char letra3 = 'L';
        char letra4 = 'A';
        char letra5 = 'N';
        char letra6 = 'C';
        char letra7 = 'I';
        char letra8 = 'A';

        printf("%c%c%c%c%c%c%c%c\n", letra1, letra2, letra3, letra4, letra5, letra6, letra7, letra8);
    }

Declarando um array:

    #include <stdio.h>

    int main() {
        int notas[10];

        notas[0] = 10;
        notas[2] = 9;
        notas[3] = 8;
        notas[9] = 4;

        printf("notas %d %d %d", notas[0], notas[2], notas[9]);
    }
