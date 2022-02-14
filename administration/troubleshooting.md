conexãomáquinaresponsávelé## Troubleshooting

### `who`  
Mostra as conexoes feitas na maquina.  
```sh
who -s 
who -b  # horario de inicializacao
who -q  # total de users na maquina
```

### `telnet`
Usado para teste de funcionamento de servicos. Considerado inseguro pois o tramite de dados acontece em plain-text.  
```sh
telnet 172.104.18.56 2021
```
  
### `finger`
Coleta dados de conexao, login e arquivos relacionados a acesso.  
```sh
finger rafael
```  
_E aconselhavel nao ter o servico finger instalado na maquina pois ele pode ceder informacoes de acesso dos usuarios e com isso trazer possiveis vulnerabilidades de acesso._  

### `ftp`
Servico de transferencia de arquivos.  
```sh
ftp 172.104.18.56
```  
  
### `whoami` ou `who i am`
Mostra o nome do usuario e o IP de quem esta fazendo conexao.  
  
## `cat /etc/resolv.conf`
Arquivo responsavel por auto-completar os dominios usados no comando `ping` por exemplo. Para editar isso podemos colocar o nome do dominio da maquina no arquivo `/etc/hosts`, veja:  
```vim
192.168.1.22 <nome-dominio> <nome-curto|apelido>
# exemplo
192.168.1.22 cobaia.mattos.com cobaia
```  
Quando executamos o comando `ping`:  
```sh
PING cobaia.mattos.com (192.168.1.22) 56(84) bytes of data.
64 bytes from cobaia.mattos.com (192.168.1.22): icmp_seq=1 ttl=64 time=0.145 ms
64 bytes from cobaia.mattos.com (192.168.1.22): icmp_seq=2 ttl=64 time=0.198 ms
64 bytes from cobaia.mattos.com (192.168.1.22): icmp_seq=3 ttl=64 time=0.187 ms
64 bytes from cobaia.mattos.com (192.168.1.22): icmp_seq=4 ttl=64 time=0.178 ms
^C
--- cobaia.mattos.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3059ms
rtt min/avg/max/mdev = 0.145/0.177/0.198/0.019 ms
```  
Note que ele identificou o apelido para o host e mostrou o dominio que ele ocupa.  
  
## `hostname` ou `dnsdomainname`
Retorna o hostname da maquina.  
```sh
hostname -f | -d
# ou
dnsdomainname
# ou
hostnamectl   # mostra infos sobre hostname, OS, versoes, etc...
```
  
## `write`
Conseguimos interagir com os usuarios conectados na maquina em modo texto.  
```sh
write root tty1   # envia mensagens em modo texto para o terminal do root
wirte rafael pts/0  # envia mensagem para o user rafael no terminal pts/0
```  
_Para saber qual user esta em qual terminal da maquina usamos o comando `w`._  
  
*Como faco para enviar mensagens para todos os usuarios logados na maquina?*  
Use o comando `echo "Mensagem para todos" | wall`

## `df`
Mostra espaco em disco
  
## `free`
Mostra o uso de memoria.
  
## `top`
Lista os processos sendo executados.  
  
## Servidor web inoperante
Fique atento a gravacao de logs, geralmente servidores web como Apache e Nginx param suas operacoes quando o espaco de armazenamento de logs nao eh suficiente.  

## Servidor Web Lento
Pode ser processos que estajam utilizando CPU demais, causando um load alto.  
  
As vezes o problema nao pode estar na maquina e sim na rede. Podemos utilizar a ferramenta `dmesg` para visualizar os logs de conexao. Verifique a comunicacao de rede fisica, cabos, switches, roteadores.  
  
Em caso de brute-force podemos rejeitar chamadas de hosts maliciosos. Para isso podemos configurar o firewall da maquina.  
