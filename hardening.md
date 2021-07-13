## Hardening
Hardening é uma maneira de melhorar o sistema operacional em termos de segurança.
  
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

