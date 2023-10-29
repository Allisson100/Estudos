# Adicionando e alterando

    const pessoa = {
        nome: "Luma",
        profissao: "Engenheira",
    }

Podemos adicionar uma nova propriedade nesse objeto da seguinte forma:

    pessoa.telefone = "11 55989159"

Agora nosso objeto está dessa forma:

    const pessoa = {
        nome: "Luma",
        profissao: "Engenheira",
        telefone: "11 55989159",
    }

E para modificar um campo que já existe:

    pesoa.nome = "Luma Silva"

E teremos o objeto atualizado:

    const pessoa = {
        nome: "Luma Silva",
        profissao: "Engenheira",
        telefone: "11 55989159",
    }

Para deletar uma propriedade também é simples:

    delete pessoa.telefone

E teremo isso:

    const pessoa = {
        nome: "Luma Silva",
        profissao: "Engenheira",
    }

Quando deletamos pdemos armazenar um valor booleano para sabermos caso quisermos se o valor foi deletado:

    const foiDeletado = delete pessoa.telefone //true ou false
