## Domain Name Server (DNS)
O DNS é uma forma amigavel de "traduzir" o endereço de um host.  
  
As configurações de DNS do seu host geralmente ficam no arquivo `/etc/resolv.conf`.  
Podemos adicionar mais clientes de DNS na nossa máquina colocando o IP do resolvedor DNS. Veja o exemplo:  

```vim
nameserver 1.1.1.1 # resolvedor cloudflare...
nameserver 8.8.4.4 # resolvedor google...
```
  
## Comando `host`
Com esse comando podemos ver o endereço principal do host. Podemos saber também se determinado host possui sistema de redundancia quando mais de um endereço é apresentado na saída do comando.

```sh
host www.itau.com.br
```
