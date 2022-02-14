conexãoé## Comandos sobre redes no Linux
O comando mais utilizado eh o `ip`
  
## `ip`
```sh
ip addr show # lista as placas de redes com os enderecos atribuidos
```
  
Podemos adicionar mais de um IP a um host usando o seguinte comando.  
```sh 
sudo ip addr add 192.168.12.140 dev wlan0
```
  
## `ping`
Com esse comando podemos ver a latencia da conexao entre os hosts. Geralmente os provedores criam CDNs para reduzir esse tempo de conexao.
```sh 
ping # verifica a comunicacao com outro host
```
Para usar no formato IPv6 basta usar o comando `ping6`
  
## `traceroute`
Mostra o caminho que o pacote faz até chegar ao destino final (o host requisitado).  
``` sh
traceroute www.wikipedia.com
```
Para usar no formato IPv6 basta usar o comando `traceroute6`.  
  
## `mtr`
É uma versão gráfica do comando `traceroute`. Além disso ele mostra outras métricas como latencia média e porcentagem de perda de pacotes.    
``` sh
mtr www.google.com
```
  
## Importante
O endereco local de um host sempre sera 127.0.0.1.  
O comando `ifconfig` nao mostra todos os enderecos IPv4 do host. 
O comando `traceroute` utiliza TTL na comunição, caso queira verificar falha na conexão com determinado host é melhor utilizar o comando `ping`.   
