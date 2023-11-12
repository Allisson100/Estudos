# Alocação dinâmica de memória

Fizemos algumas alterações no código para caso quisermos mudar o tamanho do mapa no futuro.

Primeiro no arquivo mapa.txt acrescentamos quantas colunas e quantas linhas vão ter nosso mapa:

    5 10
    |--------|
    |...|..-.|
    |..-|.@..|
    |......-.|
    |--------|

Depois no código mudamos a variável mapa, pois não sabemos quanto de memoria essa matriz vai ter, pis queremos fazer isso dinamicamente, pois como comentei, pode ser que no futuro a gente queira mudar o tamanho do mapa.

    char** mapa;

Depois criamos:

    mapa = malloc(sizeof(char*) * linhas);
    for(int i = 0; i < linhas; i++) {
        mapa[i] = malloc(sizeof(char) * (coluna + 1));
    }

A função malloc serve para alocar memoria dinamicamente, então primeiro alocamos a memoria nas linhas e depois nas colunas.

E assim como não podemos esquecer de fechar um arquivo no caso do file, aqui também temos que limpar a alocação de memória:

    for (int i = 0; i < linhas; i++) {
        free(mapa[i]);
    }

    free(mapa);

E aqui primeiro limpamos a memória da coluna e depois das linhas.

Vale lembrar que uma matriz é como se tivessemos um array e depois dele varios outros array, tipo subarrays, então é como se o array principal fosse a linha e os subarray presentes naquele array principal fosse as colunas.
