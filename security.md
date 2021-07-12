## Seguranca
_Como definir o acesso de usuarios em uma maquina?_  
Podemos usar o arquivo de configuracao chamado `/etc/securetty`. Esse arquivo lista os terminais que o usuario root tem permissao para executar.  
  
Podemos ver os comandos que um user faz no terminal digitando o comando `w`.  
```sh
w   # sim, o comando eh a letra 'w'
```  
  
Atraves desse comando podemos ver quais terminais conectados a maquina estao abertos. E por motivos de seguranca isso deve ser veirificado.  
_Como faco para nao deixar um terminal aberto sem querer?_  
Podemos executar `export TMOUT=100`, esse tempo eh medido em segundos.  
  
Podemos bloquear o acesso do root ao terminal principal `tty1`. Para isso editamos o arquivo `/etc/securetty`.  
```vim
# Virtual consoles
#tty1
tty2
tty3
tty4
tty5
```  
  
_Onde encontro os logs de login dos usuarios?_  
Podemos encontrar os logs de login no arquivo `/var/log/auth.log`.  
  
## Restringindo acesso por SSH
Podemos configurar isso atraves dos arquivos `/etc/ssh/sshd_config`.  
``` vim
# Authentication:  
AllowUsers root rafael joao  # diz quais users podem logar na maquina
PermitRootLogin   # habilita login de user root
```  
Apos configurar o arquivo execute o comando `sshd -t` para verificar se ha problemas de configuracao no arquivo e logo em seguida atualizamos a configuracao com `systemctl restart sshd`.  
  
Podemos restringir acesso por host e por usuario.
``` vim
# Authentication:  
PermitRootLogin prohibit-password   # login do root somente com chaves
```   
  
Podemos evitar o uso de senhas ao fazer login configurando:  
``` vim
# Authentication:  
PasswordAuthentication no   # login somente com chaves e certificados
```   
_Com isso evitamos o problema de ataques brute force na maquina._  
  
## TCP Wrappers
Existem dois arquivos de configuracao chamados `/etc/hosts.allow` (hosts que tem permissao de conectar na maquina) e `/etc/hosts.deny` (hosts que nao tem permissao).  

No arquivo `/etc/hosts.allow` podemos liberar os seguintes acessos de hosts:  
```vim
sshd: LOCAL   # apenas hosts locais
# ou
sshd: 127.0.0.1, 192.168.1.22
```  
Com isso podemos bloquear acesso por hosts!
  
## Firewall
Podemos permitar acesso a determinados servicos na maquina local.  
A ordem de verificacao de acesso sera:  
#### Firewall -> TCP Wrappers -> SSHD
  
Podemos configurar o firewall da maquina atraves da ferramenta `iptables`.  
```sh
iptables -L -n    # lista as regras de firewall
iptables -A INPUT -s 172.104.13.37 -p tcp --dport 22 -j DROP    # bloqueia chamadas na porta 22 com protocolo tcp para o host 172.104.13.37
iptables -D INPUT 1    # apaga a regra numero 1
```

## Importante
SEMPRE LOGUE COM DOIS TERMINAIS POIS SE DER PROBLEMA COM UMA SESSAO VOCE PODERA CONSERTAR USANDO O OUTRO TERMINAL LOGADO.  
