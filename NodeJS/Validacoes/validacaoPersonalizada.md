# Validação personalizada

Criamos uma validação personalizada com o Mongoose, pois essa é uma opção caso a gente precise de uma lógica diferente ou usar alguma biblioteca externa para fazer a validação. Então usamos como exemplo o campo de numero de paginas do arquivo Livro.js:

    numeroPaginas: {
        type: Number,
        validate: {
            validator: (valor) => {
                return valor >= 10 && valor <= 5000;
            },
            message: "O número de páginas deve estar entre 10 e 5000. Valor fornecido: {VALUE}"
        }
    }

Usamos a propriedade validate e de podemos passar um objeto com as propriedades validator que é a nossa função onde entrará com a lógica de validação e message que é onde criamos as mensagens de validação.

