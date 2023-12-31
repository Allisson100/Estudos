# O que é um middleware?

Como vai funcionar o Middleware no redux.

Basicamente o componenete React vai fazer um dispatch, mas antes de chegar na store o middleware vai interceptar esse dispatch, então ele vai fazer uma requisição na API e com a response da API ele irá fazer um novo disptach e o reducer vai pegar esses dados e vai salvar no state da store e com isso o componente React será renderizado novamente com os dados que vieram da API e com isso temos um sistema mais robusto e deixamos a responsabilidade de pegar os dados da API diretamente com o Redux e não com o componente React.