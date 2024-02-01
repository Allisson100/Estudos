# Configurando o ESLint

Utilizamos no terminal:

    npm init @eslint/config

Depois de rodarmos esse comando precisamos responder algumas perguntas para configuração nosso padrõa de desenvolvimento.

Depois digitamos:

    npx eslint ./src --fix

Dessa forma estamos dizendo que queremos que o eslint formate todos os arquivos da pasta src para a formatação que configuramos.

Instalamos também a extensão do ESLint para nos auxiliar em possíveis erros.

Agora falta apenas configurar a extensao para que os arquivos sejam salvos no padrõa que configuramos.

Para isso apertamos ctrl + shift + p. Digitamos settings, selecionamos abrir preferência do usuário e no final do arquivo adicionamos esse tipo de configuração:

    "editor.codeActionsOnSave": {
        "source.fixAll.eslint": true
    }



