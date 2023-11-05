# Entendendo os ponteiros

Utilizamos o &nome_vriavel para pegarmos o endereço de memória daquela variável e devemos passar isso para a função, pois assim vamos trabalhar com a mesma varoável e não com a cópia da variável.

E na função devemos utilizar o \* exemplo:

    void calcula (int* c) {
        // faz alguma coisa com a variável C
    }

    int c = 10;

    calcula(&c);

O \* serve para dizer que a função vai receber o endereço de memória d eum inteiro, mas poderia ser qualquer tipo de dado como o double.

Agora pa usarmos a variável c do nosso exemplo fazemos o seguinte:

    void calcula (int* c) {
        (*c)++;
    }

Devemos usar dessa forma, pois queremos acrescentar 1 no valor que está naquele endereço de memória, se simplesmente a gente colcar c++ ele vai aumentar em 1 o endereço de memória e não o valor da variável.
