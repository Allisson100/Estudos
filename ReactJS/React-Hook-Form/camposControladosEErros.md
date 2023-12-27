# Para saber mais: campos controlados

No vídeo passado, colocamos todos os campos do nosso formulário como required (obrigatório), isso fez com que caso o campo não seja preenchido, o próprio react-hook-form foque no primeiro campo não preenchido, mas mesmo assim ele ainda está em azul, por que?

Isso acontece pois a estilização do nosso input foi criado por nós mesmos, e ele não tem nenhuma estilização específica se um campo está inválido ou não.

Para começar, o useForm nos dá muitas informações legais, e uma delas é um objeto chamado formState, que tem o estado atual de todos os nossos campos, se ele é válido ou não, se está com erro ou não etc.

Para pegar os erros atuais dos nossos campos, vamos fazer isso:

    const { register, handleSubmit, formState } = useForm({
        defaultValues: {
            categoria: ''
        }
    });

    const { errors } = formState;

Aqui, errors é um objeto que contém todos os nossos campos como chaves, e como valor um outro objeto que tem várias informações. 

Neste caso, todos os nossos campos estão com erro, então se existir errors.nome, por exemplo, significa que o campo nome está com erro, então isso é mais uma coisa que o react-hook-form nos auxilia!

Para conseguirmos mostrar em tela que o input está com erro, faremos duas coisas:

- Colocar o outline do campo em vermelho;
- Criar uma mensagem personalizada para cada campo e mostrar na tela.

## Colocar o outline vermelho

Para isto, vamos primeiro criar uma classe nova dentro de Anuncie.module.scss chamada input-erro, dentro da classe formulário:

.formulario {
    …
        .input-erro {
            outline: 2px solid red;
        }
    }

OBS: colocar dentro de formulário é importante, pois senão ela não vai sobressair sobre a outra.

Agora, voltando para o formulário, temos que colocar essa classe apenas se o campo estiver com erro, como o objeto errors já nos dá isso, o código ficará assim:

    export default function Anuncie() {
        const categorias = useSelector(state => state.categorias.map(({ nome, id }) => ({ nome, id })));
        const { register, handleSubmit, formState } = useForm({
            defaultValues: {
            categoria: ''
            }
        });
        const { errors } = formState;

        function cadastrar(parametro) {
            console.log('parametro: ', parametro);
        }

        return (
            <div className={styles.container}>
                …
                <input className={errors.nome ? styles['input-erro'] : ''} {...register('nome', { required: true })} placeholder='Nome do produto' alt='nome do produto' />
                …
            </div>
        )
    }

Com isto, sempre que existir errors.nomeDoInput, ele irá mostrar o outline vermelho. Replique isto para todos os campos, lembrando de sempre colocar errors. junto com o nome do campo atual.

## Criar uma mensagem personalizada para cada campo e mostrar na tela

Estamos mostrando o erro na tela, mas qual erro que deu?

Para isso, vamos criar uma mensagem personalizada com o erro!

Primeiro, vamos criar um estilo para a mensagem de erro. Entre em Anuncie.module.scss e coloque:

    .formulario {
        …
        .mensagem-erro {
            color: red;
        }
    }

Criada a classe mensagem-erro, volte no formulário.

Agora, vamos criar uma mensagem personalizada para cada campo. Para isto, iremos utilizar o próprio required que utilizamos para dizer que o campo é obrigatório, mas ao invés de true, colocaremos a mensagem que queremos, ficando assim:

    …
    <input className={errors.nome ? styles['input-erro'] : ''} {...register('nome', { required: 'O campo nome é obrigatório' })} placeholder='Nome do produto' alt='nome do produto' />
    …

Replique isso para os outros campos com a mensagem que preferir. Agora, sempre que o campo estiver com o erro que é obrigatório (especificamente), ele irá colocar este erro dentro de errors.{nomeDoCampo}.message!Caso você ainda esteja dando console.log no errors, recarregue a página e clique no botão de submit e verá que dentro de message agora estará a mensagem, não só uma string vazia!

Agora, para utilizar esta mensagem, faça isso:

    …
    <input className={errors.nome ? styles['input-erro'] : ''} {...register('nome', { required: 'O campo nome é obrigatório' })} placeholder='Nome do produto' alt='nome do produto' />
            {errors.nome && <span className={styles['mensagem-erro']}> {errors.nome.message} </span>}
    …

Replicando isto para todos os campos, sempre que algum campo estiver com erro, tanto o outline será vermelho quanto a mensagem aparecerá logo abaixo do campo!