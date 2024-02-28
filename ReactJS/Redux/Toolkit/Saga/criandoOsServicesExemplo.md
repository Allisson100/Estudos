# Criando os services

Criamos alguns services novos, pois modificamos nossos dados do arquivo db.json para que ter dados de usuarios, cartoes e bandeiras desses cartões.

Então dentro da pasta services criamos os arquivos:

usuario.js:

    import instance from "common/config/api"

    const usuariosServices = {
        buscarPorId: async(id) => {
            const resposta = await instance.get(`/usuarios/${id}`)

            return resposta.data
        }
    }

    export default usuariosServices

Aqui nada mais do que a requisição para uma rota pelo axios, onde passamos o id junto na url.

cartoes.js:

    import instance from "common/config/api"

    const cartoesService = {
        buscarPorIdUsuario: async(usuarioId) => {
            const resposta = await instance.get(`/cartoes?usuarioId=${usuarioId}`)

            return resposta.data
        }
    }

    export default cartoesService

Aqui segue a mesma ideia do arquivos usuarios.js. Porém nesse caso estamos passando o usuarioId através de query.

bandeiras.js:

    import instance from 'common/config/api';

    const bandeirasService = {
        buscarPorId: async bandeiraIds => {
            const query = new URLSearchParams();
            bandeiraIds.forEach(id => query.append('id', id));
            const resposta = await instance.get(`/bandeiras?${query.toString()}`);

            return resposta.data;
        }
    }

    export default bandeirasService;

Nessa caso é um pouco diferente, pois criamos um async onde ele vai percorrer um array e para cada item do array ele deve adicionar os ids de cada item nessa query.

Para isso utilizamos:

    const query = new URLSearchParams();

E utilizamos:

    bandeiraIds.forEach(id => query.append('id', id));

Isso faz com que conseguimos passar para a query cada is de usuário e por fim:

    const resposta = await instance.get(`/bandeiras?${query.toString()}`);

Passamos como query todos esses ids transformando eles em string, ou seja, primeiro criamos a const query, depois utilizamos o forEach para acessar cada id dos itens e colocá-los dentro da query e depois mandamos tudo isso como query na url.
