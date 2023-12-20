# Verificando ID

Apenas criamos algunmas verificações nos controlers que utilizam ID:

    function getLivro(req, res) {
        try {
            const id = req.params.id

            if (id && Number(id)) {

                const livro = getLivrosPorId(id)
                res.send(livro)
            } else {
                res.status(422)
                res.send('Id inválido')
            }

        } catch (error) {
            res.status(500)
            res.send(error.message)
        }
    }

Aqui temos um if que verifica se o id existe e se ele é um numero.

Utilizamos um Number(id), pois sempre que for um número ele vai retornar o número, então será true e caso não for vai retornar um NaN que será um false.

# Body incorreto

Criamos apenas uma verificação de body:

    function postLivro(req, res) {
        try {

            const livroNovo = req.body

            if(req.body.nome) {

                insereLivro(livroNovo)
                res.status(201)
                res.send('Livro inserido com sucesso!')

            } else {
                res.status(422)
                res.send('O campo nome é obrigatório')
            }
        } catch (error) {
            res.status(500)
            res.send(error.message)
        }
    }

Como que queremos que todo livro novo tenha um nome, então fizemos a verificação do req.body.nome, caso não existir ou ser vazio ele cai no else e envia a mensagem de erro.