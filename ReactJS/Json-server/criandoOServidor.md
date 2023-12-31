# Criando o servidor

Vamos utilizar uma biblioteca chamada json-server para simular um back-end para nosso projeto, porém só é possível fazer requisições do tipo get com ele.

Vamos criar um arquivo na raiz do projeto chamado db.json. 

No nosso arquivo db.json temos os memos itens de categorias e itens, mas em formato json:

{
    "categorias": [
      {
        "nome": "Eletrônicos",
        "thumbnail": "/assets/categorias/thumbnail/eletronicos.png",
        "header": "/assets/categorias/header/eletronicos.png",
        "id": "eletronicos",
        "descricao": "Os melhores e mais atuais dispositivos eletrônicos estão aqui!"
      }
    ]
    "itens": [
      {
        "id": 1,
        "titulo": "Assistente virtual",
        "descricao": "Conheça nosso smart speaker de maior sucesso ainda melhor. O novo design de áudio com direcionamento frontal (1 speaker de 1,6\") garante mais graves e um som completo.",
        "foto": "/assets/itens/assistente-virtual-tela.png",
        "favorito": false,
        "preco": 285,
        "categoria": "eletronicos"
      }
    ]
}

Claro que tem muito mais itens, mas coloquei apenas a estrutura do arquivo.

Então vamos instalar a biblioteca:

    yarn add json-server

E criamos o script server para rodar nosso arquivo db corretamente no servidor:

    "scripts": {
        "start": "react-scripts start",
        "build": "react-scripts build",
        "test": "react-scripts test",
        "eject": "react-scripts eject",
        "server": "json-server --watch db.json --port 3001"
    },

Colocamos o --port para especificar a porta 3001 em nosso servidor já que por padrão ele vem com a 3000, mas a 3000 está com nosso servidor React.

E agora na rota:

    http://localhost:3001/categorias
    http://localhost:3001/itens

Podemos ver nossos itens e categorias.