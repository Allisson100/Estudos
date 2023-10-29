# As funções rand e srand

Colocamos um sitema randomico em nosso jogo para que o número secreto seja sempre diferente.

A lógica está aqui:

    int segundos = time(0);
    srand(segundos);

    int numerogrande = rand();
    int numerosecreto = numerogrande % 100;

A função rand() nos retorna um número aleatório, porém esse número sempre será igual, isso porque a "seed" que está presente na fórmula sempre é a mesma.

Então usamos um função chamada srand() que altera essa seed.

Para que o valor da seed sempre seja diferente acrescentamos em srand() a variável segundos. Essa variável segundos é obtida através da função time(0), esse time(0) é a quantidade de segundos que existe entre a data atual e a data de 1 de Janeiro de 1970, ou seja, a variável segundos sempre é diferente e consequentemente seed da formula rand() também sempre será diferente.
