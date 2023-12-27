# Reaproveitando o input

Criamos um componente chamado Input para utilizar no nosso código tanto na parte de edição do componente quanto na paste de anuncie, porém esse componente é um pouco diferente:

    import { forwardRef } from 'react'
    import styles from './Input.module.scss'

    function Input({ value , onChange , ...outrosProps }, ref) {
        return (
            <input 
                ref={ref}
                value={value} 
                onChange={onChange} 
                {...outrosProps}
                className={styles.input}
            />
        )
    }

    export default forwardRef(Input)

O react-hook-form trabalha com referencia e não fica renderizando os input conforme a gente vai digitando nele, isso é a forma como essa biblioteca trabalha.

Porém teoricamente não pe possível passar uma ref como props, mas sempre tem um jeito de resolver os problemas e nesse caso o próprio React nos da a solução que é o uso do forwardRef(Input), que é a forma difirente de exportar um componente.

Não só isso, quando usamos o forwardRef() também temos acesso a uma propriedade chama ref que chamamos ela da seguinte forma, logo após as props padrões:

    function Input({ value , onChange , ...outrosProps }, ref)

E no nosso componente passamos a ref dessa forma:

    <input 
        ref={ref}
        value={value} 
        onChange={onChange} 
        {...outrosProps}
        className={styles.input}
    />

Criamos o componente dessa forma justamento por conta do react-hook-form, mas vale lembrar que no caso do Input que existe dentro do modo de edição do item, ele não vai passar nenhuma referência para o componente, ou seja, será uma ref undefined, mas isso não terá problema e o React só usar uma ref caso ela existir, então por isso podemos reaproveitar um componente em diversos casos diferentes.

Ou detalhe interessante é como utilizamos o spread operator para passar as props:

    {...outrosProps}

Ou seja, as props ref, value e onChange sempre serão passadas, lembrando que ref undefined ele ignora, mas caso tenha outras props como nesse caso tem o alt e o placeholder, ele coloca ali.

# Dispatch / action

Agora temos que criar a action para fazer esse mudança de titulo no modo edição.

    const componenteModoDeEdicao = <>
        {modoDeEdicao
            ? <AiOutlineCheck 
                {...iconeProps} 
                className={styles['item-acao']} 
                onClick={() => {
                    setModoDeEdicao(false)
                    dispatch(mudarItem({
                    id,
                    item: {titulo: novoTitulo}
                    }))
                }}
            />
            : <AiFillEdit 
                {...iconeProps} 
                className={styles['item-acao']} 
                onClick={() => setModoDeEdicao(true)}
            />
        }
    </>

Fizemos uma alteração na const componenteModoDeEdicao, agora o onCLick chama duas funções, tanto o setModoEdicao como o disptach para a action mudarItem. Vale lembrar que o payload da action só consegue receber um item, por isso colocamos um objeto contendo o id e o item que contem o titulo nele.

Nossa action no reducer de itens ficou dessa forma:

    mudarItem: (state , { payload }) => {
        console.log(payload);
    }

Por enquanto só mostra o payload no console, mas logo vamos alterar o estado.
