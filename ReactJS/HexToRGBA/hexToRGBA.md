# HexToRGBA

HexToRGBA é uma biblioteca para converter uma cor hexadecimal para rgba, isso é interessante quando quisermos aplicar uma opacidade na cor, mas utilizá-la sem opacidade em outro lugar:

    npm install --save hex-to-rgba

Para utilizá-lo basta importar:

    import hexToRgba from 'hex-to-rgba';

E conseguimos utilizá-lo da seguinte maneira:

    hexToRgba('112233'); // "rgba(17, 34, 51, 1)"
    hexToRgba('#112233'); // "rgba(17, 34, 51, 1)"
    hexToRgba('112233', '0.5'); // "rgba(17, 34, 51, 0.5)"
    hexToRgba('#112233', 0.75); // "rgba(17, 34, 51, 0.75)"

Exemplo no componente:

    <section
        style={{ backgroundImage: 'url(/imagens/fundo.png)', backgroundColor: hexToRgba(time.cor, 0.5) }}
    />
