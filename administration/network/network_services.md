## Servicos de Rede
Eh um programa instalado na maquina que fica escutando uma determinada porta para prover comunicacao de um servico. Exemplos:  
- Webserver na porta 80
- HTTPS na porta 443
- SSH na porta 22
- FTP na porta 21
- SMTP na porta 25
- POP na porta 110
- IMAP na porta 1443
  
Esses servicos podem ser executados como deamons (ativo o tempo todo em memoria) ou inetd (chama o binario apenas quando necessario).  
  
Para listar os servicos de rede instalados na maquina fazemos:
``` sh
ss -lntp
# ou
netstat -lntp
```
  
Podemos ter uma analise melhor lendo o arquivo `/etc/services` que mostra qual servico utiliza determinada porta!  

_Posso usar a mesma porta para dois servicos web?_  
Depende, mas sera necessario desabilitar a porta de outro servico ou para o funcionamento do servico. Podemos fazer isso atraves do `systemctl`.  
  
``` sh
systemctl stop nginx
```
  
Um exemplo disso eh usar dois servicos rede web como NGINX e o Apache. Caso queira usar os dois sera necessario configurar um dos dois servicos para que atenda a porta 80 apenas quando for chamado por um endereco especifico.  
Ou seja, enquanto um escuta no 127.0.0.1:80 o outro escuta pelo 192.168.1.24:80. Um pelo endereco local e outro pelo endereco da interface.  
  
_Posso usar a mesma porta para dois servicos web?_  
*Pode, desde que nao estejam escutando no mesmo IP!*  
  
## daemon
Os servicos sao iniciado pelo systemctl automaticamente. Isso pode consumir muito da sua maquina caso o foco nao seja receber inumeras conexoes com isso podemos configurar o servico via `inetd`.  
  
```sh
sudo apt-get install telnetd
```  
  
Configuramos no arquivo `/etc/inetd.conf`.  
Podemos atraves desse arquivo executar binarios via rede!  

```vim
<num-da-porta> <tipo-socket> <protocolo> <flag> <user> <caminho-do-arquivo>
8081 stream tcp wait nobody ~/home/meu-executavel
```  
  
Depois devemos dar umrestart no servico.  
```sh
systemctl restart inedt
```

## `netcat`
considerado uma ferramente versatil para redes no Linux, nele e possivel receber e enviar dados para um host.

```sh
sudo apt-get install netcat
```
  
Nesse caso para realizar um conexao precisamos instalar o netcat tanto no host quando no client.  
```sh 
netcat -l -p 3038 # para o server
```  
e  
```sh
netcat 192.168.1.22 3038 # para o client
```  
Com isso conseguimos testar uma conexao entre duas maquinas usando o netcat.  
  
Podemos tambem chamar servicos de rede atraves do netcat.  
```sh
netcat <host> <nome-servico|numero-porta>
```  
  
## Importante
Um servico de rede nao precisa estar listado no arquivo /etc/service obrigatoriamente.  

