# Controlando o formulário

Precisamos agora controlar o estado dessse formulério e para isso vamos utilizar uma biblioteca chamada react-hook-form:

    yarn add react-hook-form

No nosso arquivo index.js do componente Anuncie digitamos:

    import { useForm } from 'react-hook-form'

    export default function Anuncie () {

        const categorias = useSelector(state => state.categorias.map(({nome,id}) => ({nome,id})))

        const { register , handleSubmit } = useForm()

        function cadastrar(parametro) {
            console.log('Parametro: ', parametro);
        }

        return (
            <div className={styles.container}>
                <Header 
                    titulo='Anuncie aqui!'
                    descricao='Anuncie seu produto no melhor site do Brasil!'
                />
                <form className={styles.formulario} onSubmit={handleSubmit(cadastrar)}>
                    <input {...register('nome')} placeholder='Nome do produto' alt="nome do Produto" />
                    <input {...register('descricao')} placeholder='Descricao do produto' alt="descrição do Produto" />
                    <input {...register('imagem')} placeholder='URL da imagem do produto' alt="URL da imagem do produto" />
                    <select {...register('categoria')}>
                        <option value="" disabled>Selecione a categoria</option>
                        {categorias.map(categoria => (
                            <option key={categoria.id} value={categoria.id}>
                                {categoria.nome}
                            </option>
                        ))}
                    </select>
                    <input {...register('preco')} type="number" placeholder="Preço do produto" />
                    <Button type="submit">
                        Cadastrar produto
                    </Button>
                </form>
            </div>
        )
    }

Como podemos ver primeiro criamos:

    const { register , handleSubmit } = useForm()

Depois em cada input utilizamos o {...register('imagem')}, utilizamos o ... , pois queremos todo o retorno dessa função. E o register recebe como parâmetro o nome do dado, ou seja, qual dado aquele input vai receber.

Depois utilizamos o handleSubmmit no onSubmmit do form:

    onSubmit={handleSubmit(cadastrar)}

E essa função que vem do rreact-hook-form recebe como parâmetro outra função, o parâmetro dessa função no mostra um abjeto com os dados do nosso formulário:

    function cadastrar(parametro) {
        console.log('Parametro: ', parametro);
    }

Terminal, exemplo:

    Parametro:  {nome: 'qwxw', descricao: 'sqws', imagem: '', categoria: 'eletronicos', preco: '123'}

Então essa biblioteca nos ajuda a controlar o estado do nosso formulário de maneira fácil e ele também tem funcionalidade de validação de formulário, mas que não vamos ver agora.