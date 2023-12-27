# Finalizando formulário

Para deixar um input obrigatório utilizndo o react-hook-form utilizamos:

    <input {...register('nome', { required: true })} placeholder='Nome do produto' alt="nome do Produto" />

Como segundo parâmetro do register, passamos um objeto com required: true.

E também arrumamos a parte do select, pois ele estava já selecionando um campo no caso Eletrônico e nós queriamos que ele ficasse como padrão a mensagem Selecione a categoria, então criamos a configuração:

    const { register , handleSubmit } = useForm({
        defaultValues: {
            categoria: ''
        }
    })

Nessa parte aqui o useForm aceita um objeto como parâmetro e nele passamos o defaultValues que é um objeto e nele devemos passar o nome do campo que no nosso caso é categorias:

    <select {...register('categoria', { required: true })}>

E passamos como vazio.

Como a nossa primeira opção do select é:

    <option value="" disabled>Selecione a categoria</option>

Então essa opção fica selecionada já que passamos vazio na configuração.

