# Conexão com o banco de dados MySQL

Como fazer uma conexão simples com o banco de dados MySQL, lembrando que temos que fazer a instalação da biblioteca mysql no projeto.

    import dotenv from 'dotenv'
    dotenv.config()

    import mysql from "mysql";

    export const db = mysql.createConnection({
        host: process.env.DB_HOST,
        user: process.env.DB_USER,
        password: process.env.DB_PASSWORD,
        database: process.env.DB_DATABASENAME,
    });

Também utilizamos o dotenv normalmente.