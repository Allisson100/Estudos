# Query para utilizar o MySQL localmente

Para conseguirmos utilizar o banco de dados MySQL diretamente em nossa máquina, devemos executar a seguinte Query:

    ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'sua_senha';
