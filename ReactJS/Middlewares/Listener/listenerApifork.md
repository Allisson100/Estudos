# Para saber mais: listenerApi.fork

Utilizaremos o fork para poder chamar a nossa api, mas o que afinal é o fork?

Começando pelo conceito de middleware, um middleware robusto (o thunk não se aplica) pode fazer não só uma tarefa, mas inúmeras tarefas diferentes. Por exemplo, você pode ter uma aplicação que em uma tarefa atualiza a API, atualiza uma API de histórico do que foi feito, adiciona o que foi feito em um analytics ou em um gerenciados de eventos. Várias tarefas podem ser feitas em uma só chamada que o middleware intercepta.

É aí que entra o fork! Fork é uma “mini tarefa” que o middleware precisa fazer, e tudo que envolve tratamento de erros (try/catch) é feito pelo próprio fork.

Outra curiosidade sobre o fork também é que além dele ser uma função assíncrona, a gente pode cancelá-lo a qualquer momento! A variável que o fork retorna é um objeto que traz { result, cancel }, sendo cancel a função para cancelar a tarefa e result o resultado que ela tratá (se veio com erro, o status da chamada, os dados que vieram etc.).

Além disso, dentro dele temos uma variável api, onde podemos pausar (com api.pause), aumentar o tempo da chamada (com api.delay) e saber o status atual da promise (com api.signal).

Concluindo, podemos dizer que o fork:

- É uma mini tarefa dentro de um middleware;
- Trata erros de forma automática (não precisamos usar try/catch);
- Podemos pausar, cancelar ou aumentar o tempo da chamada com o delay;
- Recebemos na variável do fork uma função para cancelar e um objeto com o resultado do fork.

Mesmo sendo um código pequeno na prática, ele é muito útil para as chamadas de API que precisamos fazer.