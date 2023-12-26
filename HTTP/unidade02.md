# Entendendo URLs / Acessando diferentes portas / Entendendo domínios

## Anotações Unidade 02

## Aula 01 (Entendendo URLs)

URL (Localizador de Recursos Universal)

Exemplo:

    http://localhost:3000/

    http -> Protocolo
    //localhost:3000 -> Servidor e porta
    / -> Caminho (raiz)

## Aula 02 (Acessando diferentes portas)

### Portas padrão

- 80: Padrão HTTP
- 443: Padrão HTTPS
- de 1023* até 65535: Livres para uso

* portas entre 0 e 1023 são reservadas para serviços padronizados.

## Aula 03 (Entendendo domínios)

DNS (Sistema de Nomes de Domínios)

google.com -> 142.251.128.14

### DNS em detalhe

Temos um servidor DNS que tem uma tabela gigante que associa o nome do domínio com os IPs.

Então basciamente o usuário atrvés da barra de pesquisa vai peguntar qual é o endereço de IP do site google.com, o servidor DNS vai devolver o número e com isso conseguimos estabelecer uma conexão HTTP com os servidores do google.

Podemos utilizar o nslookup para descobrir o endereço IP dos websites.

O DNS é hierárquico

    raiz -> com
        -> br
        -> org
        -> net
        -> ...
