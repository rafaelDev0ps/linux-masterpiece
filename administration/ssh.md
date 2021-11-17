## Como funcionam um servidor SSH?
Primeiro precisamos instalar um pacote chamado `openssh-server`.  
```console
$ sudo apt-get install openssh-server
```  
  
Apos a instalacao verifique se a porta SSH de numero 22 esta aberta.  
```console
$ sudo ss -lntp
State       Recv-Q           Send-Q                Local Address:Port                  Peer Address:Port         Process                                                         
LISTEN      0                4096                  127.0.0.53%lo:53                    0.0.0.0:*                 users:(("systemd-resolve",pid=722,fd=13))                      
LISTEN      0                128                   0.0.0.0:22                          0.0.0.0:*                 users:(("sshd",pid=799,fd=3))                                  
LISTEN      0                128                   [::]:22                             [::]:*                    users:(("sshd",pid=799,fd=4))
```  
  
Para testar a conexao com o SSH basta usar o `localhost`.  
```console
$ ssh localhost
```  
Para acessar um servidor via SSH eh necessario realizar um login com usuario/senha ou atraves de uma chave publica.  
  
### Criando chave privada para SSH
Para gerar uma chave iremos usar uma ferramenta chamada `ssh-keygen`.  
```console
$ ssh-keygen
  
Generating public/private rsa key pair.
Enter file in which to save the key (/home/rafael/.ssh/id_rsa): 
Created directory '/home/rafael/.ssh'.
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/rafael/.ssh/id_rsa
Your public key has been saved in /home/rafael/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:N5C+nZU1Evk6uU2/vQvy/qhc//ttN9DxQW+ZQznQDQ8 rafael@cobaia
The key's randomart image is:
+---[RSA 3072]----+
|            .oE.o|
|         .  .. O.|
|        o   ..= *|
|       . .   +.Bo|
|        S o oo..=|
|         + ++....|
|        . o. B.. |
|          . = =.*|
|           oo+.O#|
+----[SHA256]-----+
```  
  
Note que foi gerado uma chave publica (`id_rsa.pub`) e uma chave privada (`id_rsa`). Para que outros consigam acessar o servidor SSH eh necessario ter acesso a chave publica.  
  
Depois de criar a chave eh necessario habilitar ela para futuras conexoes. Para isso fazemos:  
```sh
$ ssh-copy-id -i /caminho/da/chave nome_do_user@ip_da_maquina
$ # exemplo
$ ssh-copy-id -i ~/.ssh/chave.pub rafael@192.168.0.11
```  
  
Dessa maneira nao sera necessario realizar login, a conexao sera feita usando a chave publica criada e habilitada.  
  
### Gerenciando chaves SSH
Usamos o comando `ssh-add` para gerenciar as chave publicas existentes na maquina do cliente.  
```console
$ ssh-add -L    # lista as chaves publicas na memoria
# ssh-add -D    # deleta todas as chaves publicas armazenadas
```  
  
### Gerenciando acesso de usuarios via SSH
Gerenciamos os usuarios atraves do arquivo `/etc/ssh/sshd_config`.  
Por padrao todos os users sao permitidos com excessao o root. Para restringir essa lista voce precisa adicionar o seguinte comando seguido dos nomes dos users.  
```config
AllowUsers rafael root joao
  
# ou podemos restringir acesso
DenyUsers pedro roberto
```  
Apos isso reinicie o servico `sshd` atraves do comando `systemctl restart sshd`.  
Dessa forma somente os users `rafael`, `root` e `joao` irao conseguir realizar conexoes SSH.  
  
Podemos tambem utilizar esse conceito para grupos usando as chaves `AllowGroups` e `DenyGroups`.  

**IMPORTANTE**  
- No servidor SSH as chaves publicas autorizadas ficam no arquivo `~/.ssh/authorized_keys`.  
- O processo `ssh-agent` eh responsavel por gerenciar as chaves.  
  
Podemos obter mais informacoes de configuracoes na criacao de uma chave usando o help do comando `ssh-keygen`. Basta usar `ssh-keygen -h`.  