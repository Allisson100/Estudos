# react-icons

É uma biblioteca de icones para usar no React.

    npm install react-icons --save

No nosso componente exportamos o icone e usamos ele como um componente:

    import {AiFillCloseCircle} from 'react-icons/ai'

    <AiFillCloseCircle size={25} className="deletar" onClick={aoDeletar} />

A propriedade size serve para redimensionar o icone.

Na parte de exportação colocamos /ai, esse ai é a pasta dos icons da biblioteca, mas para sabermos qual pasta correta exportar, basta ver as iniciais do nome do icone que nesse caso era ai. O nome do icone pegamos diretamente do site do React Icons.

Lembrando que podemos mudar as cores do icones também:

    <AiFillStar color='#F5ED00'/>
