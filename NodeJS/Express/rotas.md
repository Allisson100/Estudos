# Rotas

Como criar rotas e seus métodos.

Aquivo principal do projeto, App.js:

    import express from "express";
    import cors from "cors";

    import userRoutes from "./routes/users.js"

    const app = express();

    app.use(express.json());
    app.use(cors());

    app.use("/", userRoutes);

    app.listen(8800, () => {
        console.log("Servidor rodando!");
    });

Arquivos das do usuário, users.js:

    import express from "express";
    import { getUsers , addUser , updateUser , deleteUser } from "../controllers/users.js";

    const router = express.Router();

    router.get("/", getUsers)

    router.post("/", addUser)

    router.put("/:id", updateUser)

    router.delete("/:id", deleteUser)

    export default router

Separei cada função em uma pasta chamada cotrollers e também chamei o arquivo de user.js:

    import { db } from "../db.js";

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

Basicamente em cada método devemos passar os parâmetros necessários para que funcione corretamente.
