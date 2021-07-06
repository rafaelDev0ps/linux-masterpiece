# Redes

Quando existe uma conexao mutua entre varios computadores podemos chamar de rede, cada computador possui um endereco (um host). Esses host se comunicam atraves de um protocolo em comum que serve de regra para que a comunicacao funcione.

Os hosts podem se conectar atraves de varios meios como cabo UTP, WiFi e fibra otica.

Todo computador possui por padrao um `ip`, `netmask`, `network` e `gateway`
- `ip` endereco do host.
- `netmask` define qual parte do IP faz parte do enderecamento do host e qual parte do IP que fara parte do enderecamento da rede.
- `network` endereco que representa a rede.
- `broadcast` endereco destinado para se comunicar com toda a rede.
- `gateway` endereco que te leva para outras redes (e.g. internet)

Exemplo

| *Agente* | *Endereco* |
| --- | --- |
| IP | 192.168.32.14 |
| Netmask | 255.255.255.0 |
| Network | 192.168.32.0 |
| Broadcast | 192.168.32.255 |
| Gateway | 192.168.32.1 |

No exemplo acima podemos vir que o IP do host e 192.168.32.14 e o netmask define que os 3 primeiros blocos do endereco sao destinados a Network enquanto o ultimo bloco sera destinado para enderecar os host. Nesse exemplo esta sendo usado endereco do tipo IPv4 onde cada bloco pode de ir de 0 ate 255.

Sendo assim, com essa configuracao de netmask podemos ter 256 enderecos de host.

## Importante
Existem enderecos de IP restritos para hosts. Os que tem terminacao em 255, 0 e 1. Logo os numeros enderecaveis sao do 2 ao 254.
