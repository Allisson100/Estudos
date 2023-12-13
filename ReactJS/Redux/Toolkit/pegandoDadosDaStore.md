# Pegando dados da store

# Pegando itens

Basicamente pegamos os itens da store porém já filtrados:

    import Header from "components/Header";
    import { useSelector } from "react-redux";
    import { useParams } from "react-router-dom";
    import styles from './Categoria.module.scss'

    export default function Categoria() {

        const { nomeCategoria } = useParams()
        const { categoria , itens } = useSelector(state => {
            return {
                categoria: state.categorias.find(categoria => categoria.id === nomeCategoria),
                itens: state.itens.filter(item => item.categoria === nomeCategoria),
            }
        })

        return (
            <div>
                <Header 
                    titulo={categoria.nome}
                    descricao={categoria.descricao}
                    imagem={categoria.header}
                />
                <div className={styles.itens}>
                    {itens?.map(item => (
                        <div key={item.id}>
                            {item.titulo}
                        </div>
                    ))}
                </div>
            </div>
        )
    }

Vale ressaltar aqui que utilizamos apenas um useSelector para para buscar dois itens diferentes na store do redux.

    const { categoria , itens } = useSelector(state => {
        return {
            categoria: state.categorias.find(categoria => categoria.id === nomeCategoria),
            itens: state.itens.filter(item => item.categoria === nomeCategoria),
        }
    })

E apenas desestruturamos ele depois.

