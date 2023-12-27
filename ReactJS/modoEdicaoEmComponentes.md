# Criando modo edição

Fizemos algumas modificações no código, porém o que se deve detalhar é:

    const [modoDeEdicao, setModoDeEdicao] = useState(false)
    const [novoTitulo, setNovoTitulo] = useState(titulo)

    const componenteModoDeEdicao = <>
        {modoDeEdicao
            ? <AiOutlineCheck 
                {...iconeProps} 
                className={styles['item-acao']} 
                onClick={() => setModoDeEdicao(false)}
            />
            : <AiFillEdit 
                {...iconeProps} 
                className={styles['item-acao']} 
                onClick={() => setModoDeEdicao(true)}
            />
        }
    </>

    <div className={styles['item-titulo']}>
        {modoDeEdicao
        ? <input 
            value={novoTitulo} 
            onChange={(evento) => setNovoTitulo(evento.target.value)}
        />
        : <h2>{titulo}</h2>
        }
        <p>{descricao}</p>
    </div>

Primeiro criamos os icones para saber se aquele componente está em modo de edição ou não e colocamos ele na const componenteModoDeEdicao apenas para organização.

Ele apenas tem dois icones que quando clicamos nele, ele muda o valor da variável modoDeEdicao para true ou false.

Temos duas variáveis de estado:

    const [modoDeEdicao, setModoDeEdicao] = useState(false)
    const [novoTitulo, setNovoTitulo] = useState(titulo)

Uma para o modo de edição que já comentei e outra para conseguirmos alterar o valor do titulo.

Criamos uma condição na parte do item que mostra o titulo:

    <div className={styles['item-titulo']}>
        {modoDeEdicao
        ? <input 
            value={novoTitulo} 
            onChange={(evento) => setNovoTitulo(evento.target.value)}
        />
        : <h2>{titulo}</h2>
        }
        <p>{descricao}</p>
    </div>

Aqui caso o item não esteja em modo de edição ele vai mostrar o titulo normal, mas caso esteja em modo de edição ele vai mostrar um input e vamos controlar esse input atrvés da variável de estado novoTitulo.

Por enquanto ainda não está finalizado essa parte de edição do item.