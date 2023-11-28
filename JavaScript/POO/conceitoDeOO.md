# 1. ConceitoDeOO

# Programação orientada a objeto com Javascript

# Conceito de OO

O que são paradigmas de programação?

- Abordagens sobre como resolver problemas de programação, baseadas em uma teoria ou conjunto de princípios definidos.

Alguns paradigmas:

- Imperativo;
- Relacional;
- Declarativo;

Orientação a objetos:

Princípio de espelhar o mundo real através de uma estrutura de objetos com características e ações, que interagem uns com os outros.

Exemplo, como fazemos para abstrair um gato em código?

Características: (propriedades)

- sexo;
- idade;
- pelagem;
- status:
  - castrado;
  - vacinado;
  - vermifugado.

Comportamentos:

- miar;
- comer;
- dormir;
- limpar;
- brincar:
  - bolinh;
  - laser.

Objetos literais:

    const gato = {
        nome: 'Churrumina',
        nascimento: '25/11/2018',
        pelagem: 'mesclada',
        status: {
            castrada: true,
            vacinada: true,
            vermifugada: true
        },

        // comportamento (métodos)
        miar: function() {
            console.log('miau')
        }
    }

### Modelos de objetos

    const gato1 = {
        nome: 'Churrumina',
        nascimento: '25/11/2018',
        pelagem: 'mesclada',
        status: {
            castrada: true,
            vacinada: true,
            vermifugada: true
        },
    }

    const gato2 = {
        nome: 'Wen Ning',
        nascimento: '25/01/2021',
        pelagem: 'creme',
        status: {
            castrada: true,
            vacinada: true,
            vermifugada: true
        },
    }

Já podemos ver aqui que se formos criar uma constante para cada gato diferente, vamos ter muito problemas. Para resolver isso podemos fazer:

    const modeloGato = {
        nome: stringNome,
        nascimento: stringData,
        pelagem: stringPelagem,
        status: {
            castrada: boolCastrado,
            vacinada: boolVacinado,
            vermifugada: boolVermifugado
        },
    }

Então a partir de um modelo a gente cria dois gatos que nocaso será um array de objetos contendo nossos dois gatos.

Cada gato seria uma instância do modeloGato.

Princípios da OO:

- Classe;
- Objeto;
- Herança;
- Polimorfismo;
- Encapsulamento.
