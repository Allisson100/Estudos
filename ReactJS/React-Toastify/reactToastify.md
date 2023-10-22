# react-toastify

O react-toastify é o que faz aparecer uma mensagem quando um usuário faz uma ação no banco de dados, por exemplo deletar, dar update, obter dados ou adicionar algum dado.

Para utlizá-lo instalamos com:

    yarn add react-toastify

Utilizamos ele da seguinte forma no código

    import { toast, ToastContainer } from "react-toastify";

    return (
        <>
        <Container>
            <Title>USUÁRIOS</Title>
            <Form onEdit={onEdit} setOnEdit={setOnEdit} getUsers={getUsers}/>
            <Grid users={users} setUsers={setUsers} setOnEdit={setOnEdit}/>
        </Container>
        <ToastContainer autoClose={3000} position={toast.POSITION.BOTTOM_LEFT} />
        <GlobalStyle />
        </>
    );

Utilizamos ele como um componente e definimos alguns padrões daquela forma.

Podemos setar as mensagens assim:

    const getUsers = async () => {
        try {
            const res = await axios.get("http://localhost:8800")
            setUsers(res.data.sort((a,b) => (a.nome > b.nome ? 1 : -1)))
        } catch (error) {
            toast.error(error)
        }
    }

    const handleDelete = async (id) => {
        try {
            const {data} = await axios.delete("http://localhost:8800/" + id)
            const newArray = users.filter((user) => user.id !== id)

            setUsers(newArray)
            toast.success(data)
        } catch (error) {
            if (error.response && error.response.data) {
                toast.error(error.response.data);
            } else {
                toast.error("Erro ao excluir o item.");
            }
        }
    }

E as mensagens de sucesso obtemos assim:

    toast.success(data)

Pois recebemos essas mensagens em forma de json através das funções das rotas:

    export const getUsers = (_, res) => {
        const q = "SELECT * FROM usuarios";

        db.query(q, (err, data) => {
            if (err) return res.json(err);

            return res.status(200).json(data);
        })
    }

    export const addUser = (req, res) => {
        const q = "INSERT INTO usuarios(`nome`, `email`, `fone`, `data_nascimento`) VALUES(?)"


        const values = [
            req.body.nome,
            req.body.email,
            req.body.fone,
            req.body.data_nascimento,
        ]

        db.query(q, [values], (err) => {
            if (err) return res.json(err)

            return res.status(200).json("Usuário criado com sucesso")
        })
    }

    export const updateUser = (req, res) => {
        const q = "UPDATE usuarios SET `nome` = ?, `email` = ?, `fone` = ?, `data_nascimento` = ? WHERE `id` = ?"

        const values = [
            req.body.nome,
            req.body.email,
            req.body.fone,
            req.body.data_nascimento,
        ]

        db.query(q, [...values, req.params.id], (err) => {
            if (err) return res.json(err)

            return res.status(200).json("Usuário atualizado com sucesso")
        })
    }

    export const deleteUser = (req, res) => {
        const q = "DELETE FROM usuarios WHERE `id` = ?"

        db.query(q, [req.params.id], (err) => {
            if (err) return res.json(err)

            return res.status(200).json("Usuário deletado com sucesso")
        })
    }
