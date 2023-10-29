# O formato JSON

JS normal:

    const cliente = {
        nome: "João",
        idade: 24,
        email: "joao@frim.com",
        telefone: ["1156565656", "116565656"],
        endereco = {
            rua: "qualquer endreço aqui",
            numero: 1124,
            apartamento: true,
            complemento: "ap 934",
        }
    }

JSON:

    {
        "nome": "João",
        "idade": 24,
        "email": "joao@frim.com",
        "telefone": ["1156565656", "116565656"],
        "endereco" = {
            "rua": "qualquer endreço aqui",
            "numero": 1124,
            "apartamento": true,
            "complemento": "ap 934"
        }
    }

- Não é permitido ter uma virgula no último item
- Funções não são permitidas
- Comentários não são permitidos
- Suporta apenas tipos primitivos (string, number, booblean, null)

# Lendo um arquivo JSON

    {
        "nome": "Joao",
        "email": "joao@firma.com",
        "telefone": ["11223344", "11922334453"],
        "endereco": {
            "rua": "R. Joseph Climber",
            "numero": 202,
            "apartamento": true,
            "complemento": "ap 934"
        }
    }

Para acessá-lo digitamos:

    const dados = require("./cliente.json")

# Operações com um JSON

    const dados = require("./cliente.json")

    const clienteEmString = JSON.stringfiy(dados)

    JSON.parse(clienteEmString) // transforma essa string de novo em objeto
