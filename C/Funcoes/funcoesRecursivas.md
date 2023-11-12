# Função recursiva

Utilizamos uma função recursiva ao invés de um loop:

    void explodepilula(int x, int y, int qtd) {

        if(qtd == 0) return;
        m.matriz[x][y+1] = VAZIO;
        explodepilula(x , y+1, qtd - 1);
    }
