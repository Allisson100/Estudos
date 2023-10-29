# +Para saber mais: objeto literal e referência

O Object.create() pode nos ajudar a fazer uma cópia de outro objeto, vale ressaltar que fazr const novoObjeto = objPersonagem, só funciona com tipos primitivos do javascript, por isso utilizamos o metodo Object.create().

    const objPersonagem = {
        nome: "Gandalf",
        classe: "mago",
        nivel: "20"
    }

    const objPersonagem2 = Object.create(objPersonagem)
    objPersonagem2.nome = "Gandalf, o Cinzento"

    console.log(objPersonagem.nome) //Gandalf
    console.log(objPersonagem2.nome) //Gandalf, o Cinzento
