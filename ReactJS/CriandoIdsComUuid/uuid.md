# uuid

Essa biblioteca serve para criarmos ids para elementos sem a chance deles se repetirem.

Para instalá-lo digitamos:

    npm i uuid

Para importar ele no projeto digitamos:

    import { v4 as uuidv4 } from 'uuid';

E utilizamos ele dessa forma:

    {
      id: uuidv4(),
      nome: 'Programação',
      cor: '#57C278'
    },
