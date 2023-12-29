# Conectando MongoDB e API

Vamos instalar o mongoose:

    npm i mongoose@latest

Vale lembrar que o mongo é o nosso banco de dados e o mongoose é a interface que está nos ajudando a fazer a conexão com ele.

Criamos uma pasta chamada config dentro de src e nele criamos um arquvo chamado dbConnect:

    import mongoose from "mongoose";

    async function conectaNaDatabase() {
        mongoose.connect('mongodb+srv://aulabancoalura:joYsAhlBOvRhepi1@alurabanco.ndtdeyh.mongodb.net/livraria?retryWrites=true&w=majority')

        return mongoose.connection
    }

    export default conectaNaDatabase

Utilizamos alguns métodoa da biblioteca mongoose, e um dele foi o connect que justamente serve para conectar ao banco e colcoamos nossa string lá do mongoDB Atlas ali, mas trocamos o password pelo correto e adicionamos o nome do nosso banco também que no caso é livraria e adicionamos livraria logo após o .net/.

Depois exportamos essa função, pois ele que é responsável por fazer a conexão e vale lembrar que é uma função assincrona.

Dentro do arquivo app.js também fizemos algumas configurações:

    import conectaNaDatabase from './config/dbConnect.js'

    const conexao = await conectaNaDatabase()

    conexao.on('error', (erro) => {
        console.error('Erro de conexão', erro)
    })

    conexao.once('open', () => {
        console.log('Conexão com o banco feita com sucesso!');
    })

Primeiro importamos a função e salvamos o retorno dela em uma variável. Fazendo isso podemos ter acesso em alguns métodos.

O .on() serve para ouvir algum evento e nesse caso passamos o evento erro para sabermos logo de cara se houve algum erro ao tentar fazer a conexão.

Depois utilizamos o .once() e passamos o evento 'open' que serve para sabermos se houve uma tentativa de conexão com o banco e se deu certo essa conexão.


