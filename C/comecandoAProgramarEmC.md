# Começando a programar

Todo código C tem a extensão .c, então vamos criar um arquivo chamado programa.c.

Nesse arquivo criamos um código simples:

    #include <stdio.h>

    int main() {
        printf("Bem vindo ao nosso jogo de adivinhação");
    }

Todo programa em C tem que ter o #include <stdio.h> e também devemos colocar nosso código dentro da função main(), int main() {}.

E para executar esse código devevemos fazer alguns instalações que já fizemos antes e depois disso no nosso terminal vamos digitar:

    gcc programa.c -o programa.exe

Esse comando basicamente vai transformar no arquivo em código binário para o computador conseguir etender ele, ou seja, estamos criando um código executável agora chamdo, programa.exe.

E para executar o programa digitamos:

    ./programa.exe

E com isso já conseguimos ver nosso programa rodando no terminal
