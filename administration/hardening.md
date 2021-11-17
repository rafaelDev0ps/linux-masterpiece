## Hardening
Hardening é uma maneira de melhorar o sistema operacional em termos de segurança. Tudo o que possui uma camada de restricao na maquina pode ser considerado como hardening.
  
### Complexidade de Senhas
Aumentar o tamanho das senhas através do `libpam-cracklib`.  
```sh
sudo apt-get install libpam-cracklib
```  
  
Após isso configuramos o arquivo `/etc/pam.d/common-password`.  
```vim
# here are the per-package modules (the "Primary" block)
password	requisite			pam_cracklib.so retry=3 minlen=12 difok=3
```  
Onde retry é o número de tentativas, minlen é o tamanho mínimo da senha e difok é o número mínimo de caracteres que deve ter na senha.  
```sh
root@ubuntu:/home/ubuntu# passwd ubuntu
New password: 
BAD PASSWORD: it is too simplistic/systematic
BAD PASSWORD: is too simple
Retype new password: 
```  
  
## Expiração de contas
Podemos ver as informações de uma conta de usuário através do comando chage.  
```sh
chage -l <nome-do-user>
```

Para definir uma data de expiração de uma conta fazemos.  
```sh
chage -E 2021-12-31 <nome-do-user>
```  
Saída:  
```sh
root@ubuntu:/home/ubuntu# chage -l ubuntu
Last password change					: Apr 21, 2021
Password expires					: never
Password inactive					: never
Account expires						: Dec 31, 2021
Minimum number of days between password change		: 0
Maximum number of days between password change		: 99999
Number of days of warning before password expires	: 7
```
  
Para definir o número mínimo e máximo de dias para trocas de senhas.  
```sh 
chage -M 120 <nome-do-user>   # número maximo de dias entre troca de senhas
chage -m 2 <nome-do-user>   # número mínimo de dias entre troca de senhas
```  
Saída:  
```sh
Last password change					: Apr 21, 2021
Password expires					: Aug 19, 2021
Password inactive					: never
Account expires						: Dec 31, 2021
Minimum number of days between password change		: 2
Maximum number of days between password change		: 120
Number of days of warning before password expires	: 7
```  
  
Para mais infos use o comando `passwd --help`.  

## `/etc/login.defs`
Arquivo responsavel pelas definicoes de logins da maquina. Podemos definir as regras de definicao de senha dos usuarios nesse arquivo (exp. de senhas, min e max de dias para alterar senha, etc).

## Desativando Servicos desnecessarios
Podemos remover os servicos de rede que nao estao sendo utilizados pela maquina, com isso deixamos a maquina com menos portas abertas tornando-a mais segura.  
Alem disso podemos alterar as configuracoes padrao de acesso SSH no arquivo `/etc/ssh/sshd_config`.  

## Update de seguranca
Podemos fazer uma auditoria dos pacotes instalados na maquina. Para listar todos os pacotes instalados na maquina usamos o comando:  
``` sh
dpkg -l
```
  
Podemos configurar o arquivo de updates de seguranca chamado `/etc/apt/source.list`, nele encontramos os repositorios resposaveis pelos pacotes de seguranca.  
```vim
deb http://security.ubuntu.com/ubuntu focal-security main restricted
# deb-src http://security.ubuntu.com/ubuntu focal-security main restricted
deb http://security.ubuntu.com/ubuntu focal-security universe
# deb-src http://security.ubuntu.com/ubuntu focal-security universe
deb http://security.ubuntu.com/ubuntu focal-security multiverse
# deb-src http://security.ubuntu.com/ubuntu focal-security multiverse
```  
  
Para fazer o download e instalacao desses pacotes fazemos:  
```sh
sudo apt-get update
sudo apt-get update -f -u
reboot
```  
  
Tenha o habito de ter um backup da lista de pacotes que estao instalados na sua maquina!  
```sh
dpkg --get-selections | tee pacotes-instalados-07-2021.txt
```  
  
Podemos fazer um `diff` dos arquivos de lista de pacotes depois:  
```sh
diff lista1.txt lista2.txt
```  
  
## SUID e SGID
Podemos conferir quais arquivos binarios os usuarios podem ter acesso atraves do grupo que estao:  
```sh 
find . -perm /4000
```  
  
## ulimit
Podemos listar os limites de um user durante a sessao dele.  
```sh
ulimit -a
```  
  
Encontramos informacoes dos limites dos usuarios na sessao atraves do arquivo `/etc/security/limits.conf` listando o que significa cada restricao.  
  
```vim 
#<domain>      <type>  <item>         <value>
root            hard    nofile        1000000
```  
No exemplo acima o usuario root pode ter mais de um milhao de arquivos abertos na sua sessao.  
Caso queiramos estabelecer essa regra para um grupo basta colocar um `@nome-grupo` no dominio.  
```vim 
#<domain>      <type>  <item>         <value>
@meugrupo            hard    nofile        1000000
```  
  
## Monitoramento de logs
Podemos monitorar logs em tempo real usando a flag `-f` do `tail`.  
```sh
tail -f /var/log/auth.log   # logs de acesso
tail -f /var/log/daemon.log  # para programas que estao rodando como daemon
lastlog  # verifica quais user fizeram acesso a maquina
```  
