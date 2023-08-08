# Tipos de filtro

body {
filter: tipo do filtro;
}

### grayscale()

Este filtro converte os elementos para escala de cinza, tornando-os preto e branco. Você pode definir a intensidade do efeito usando um valor de porcentagem, onde 0% significa nenhuma conversão para escala de cinza e 100% significa uma conversão completa para escala de cinza.

### sepia()

Este filtro aplica um tom de sépia ao elemento, criando um efeito de envelhecimento ou vintage. Assim como o grayscale(), você pode definir a intensidade com um valor de porcentagem.

### blur()

O filtro blur() aplica um desfoque ao elemento, criando um efeito de borrão. Você pode definir o valor do raio do desfoque em pixels ou outras unidades.

### brightness()

Este filtro ajusta o brilho do elemento. Um valor de 0% tornará o elemento completamente preto, enquanto um valor de 100% não terá efeito. Valores acima de 100% aumentarão o brilho.

### contrast()

O filtro contrast() ajusta o contraste do elemento. Um valor de 0% tornará o elemento completamente cinza, enquanto um valor de 100% não terá efeito. Valores acima de 100% aumentarão o contraste.

### hue-rotate()

Este filtro gira os tons de cores no elemento. O valor é definido em graus, e você pode usar um número positivo ou negativo para ajustar a rotação.

### saturate()

Este filtro ajusta a saturação das cores do elemento. Um valor de 0% deixará o elemento completamente sem cor (tons de cinza), enquanto um valor de 100% não terá efeito. Valores acima de 100% aumentarão a saturação das cores.

### invert()

O filtro invert() inverte as cores do elemento, criando um efeito de negativo. O valor é definido em porcentagem e determina a intensidade do efeito.

### opacity()

Este filtro ajusta a opacidade do elemento. Um valor de 0% tornará o elemento completamente transparente, enquanto um valor de 100% não terá efeito.

### drop-shadow()

O filtro drop-shadow() cria uma sombra projetada para o elemento. Você pode definir a posição horizontal, posição vertical, desfoque e cor da sombra.

Exemplo:

    filter: drop-shadow(2px 2px 4px rgba(0, 0, 0, 0.4));
