# Arrays e ponteiros

Array é um ponteiro por natureza, por isso não precisamos passar a referência dele para a função.

E a conta que o computador faz em cima do array é a seguinte, se o endereço de memória do array é 100, o index um desse array de caracter é 101, pois cada caracter oculpa 1 byte. Se fosse no caso um array de números inteiros, seria a posição 104, pois um int tem 4 bytes.
