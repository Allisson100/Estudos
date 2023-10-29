# C A Linguagem de Programação que é uma mãe

### Tipos de dados em C

Primitivo:

- int;
- char;
- float
- double;

Derivado:

- array;
- structure;
- union;
- enum;
- pointer;

### Pimitivos

// 4 buytes
int idade = 68;

// 1 byte
char arroba = "@";

// 4 bytes (6 casas decimais)
flaot saldoNaConta = 18923.12

// 8 bytes (15 casas decimais)
double teste = 0.00001

// 4 bytes \* 7 posições = 28 bytes
int teste[7] = {19,20,21,22,23,24,25};

// 3 bytes \* 10 posições = 30 bytes
char tesrefa[3][10] = {
"Varrer",
"Louça",
"Jantar,"
}

// 15 + 4 + 4 = 23 bytes
struct canal
{
char nome[15];
int inscritos;
float mediaLikes;
}

struct canal CDFTV = {"Código Fonte TV", 222484, 97.26}

### Pointer

Pointer é uma varoável que armazena o endereço de outra variável

num - Nome da variável
10 - Valor de Num
0x7fff5694dc58 - Endereço de Num

Exemplo:

    #include <stdio.h>

    int main (){

        // Daclarção variável e ponteiro
        int ano, *pAno;

        // Inicialização
        ano = 2020;
        pAno = &ano;

        printf("%d", *pAno);
        // O valor de 'ano': 2020

        printf("%d", *&ano);
        // 2020 (também)

        printf("%u", &ano);
        // Endereço de 'ano': algo com 0x7fff5694dc58

        printf("%u", pAno);
        // Endereço de 'ano' também

        printf("%u", &pAno);
        // Endereço de 'pano' <> 'ano'

        return 0;
    }

### Modificadores em C

short , long , signed , unsigned

// De -32768 até 32767
// Ocupa só 2 bytes
short int idade = 68;

// De -9223372036854775808 aé 9223372036854775807
// Se usa 'long long' ao invés de 'long int'
long long idadeUniverso = 14000000000

// De 0 até 65535
// Ocupa só 2 bytes
short unsigned int idade = 68;

// De -128 até 127
// Ocupa 1 byte
char meuCgar;

// De 0 a 255;
// Ocupa 1 byte
unsigned char codigoASC;
