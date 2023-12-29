# Para saber mais: tipos de API

API REST é um tipo de API extremamente comum em programação web.

O termo REST (representational state transfer ou transferência de estado representacional) representa um padrão para desenvolvimento de APIs web utilizando o protocolo HTTP para transmissão de dados.

Porém, pensando que APIs são interfaces que usamos em programação, existem várias outras formas de integrar programas ou serviços diferentes, que utilizam outros protocolos de comunicação, casos de uso e modos de acesso.

APIs podem ser desenvolvidas para diversos usos, por exemplo:

- Para uso interno de uma empresa, por exemplo, para fornecer dados como um serviço para um sistema maior.

- Para uso “externo”, como quando a API é desenvolvida pela empresa como um produto para ser utilizado por clientes.

- Podem ser abertas e de uso livre, desenvolvidas para uso da comunidade, sendo muito comuns para testes ou projetos de estudo.

- Podem ser de terceiros, como as que utilizamos para integrar serviços externos aos nossos produtos.

Além de usos diversos, as APIs também podem ser desenvolvidas seguindo outras arquiteturas além do REST. Seguem alguns exemplos:

- APIs SOAP: SOAP (Simple Object Access Protocol ou protocolo simples de acesso a objetos) utiliza o formato de dados XML e pode usar HTTP ou outros protocolos na comunicação. É um formato mais antigo que o REST e muito utilizado por aplicações de grande porte, porém mais lento que o REST.

- Event-Driven APIs: APIs orientadas a eventos, ao contrário das APIs REST, não dependem de requisições feitas pelo lado cliente para iniciar a comunicação. Nesse caso, o cliente ou clientes “inscritos” na API se comunicam com ela através de gatilhos de eventos, como, por exemplo, um novo registro de usuário.

- APIs GraphQL: o GraphQL é uma linguagem de consulta (query) de APIs e também um runtime para executar estas consultas. É uma alternativa ao REST que pode se conectar a diversas APIs e bases de dados diferentes e retornar objetos complexos através de uma única requisição.

- APIs gRPC: Remote Procedure Calls (ou chamadas procedurais remotas), desenvolvido pelo Google, é um framework baseado em HTTP2 para comunicação síncrona e assíncrona, que visa facilitar comunicação rápida e simplificada entre diversos serviços.