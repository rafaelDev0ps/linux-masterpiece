padrão## Permissões

A melhor forma de ver as permissões de um arquivo é através do comando `ls`. 

As permissões são divididas em 4 partes.

#### Exemplo
```sh 
- rw- rw- r--
- r-x rw- r--
- -wx rwx r-x
```

[tipo do arquivo] [permissões do dono] [permissões do grupo] [outros]


#### No Linux existem vários tipo de arquivos:

- `-` arquivo de texto
- `l` link simbólico
- `b` dispositivo de bloco
- `s` socket
- `d` diretorios
- `c` dispositivos de caractere

#### O que significa cada letra?

- `r` (4) permissão de leitura
- `w` (2) permissão de escrita e deleção
- `x` (1) permissão de execução
- `t` (1) stick bit
- `S` (4) SUID
- `S` (2) SGID
- `-` (0) ausência de permissão

Podemos usar a forma octal de permissões que consistem em somar os valores de cada permissão. Veja os exemplos abaixo:

``` sh
- rwx rwx rwx = 7 7 7
- rw- rw- rw- = 6 6 6
- -wx r-x rw- = 3 5 6

e assim por diante...
```

## `chmod`
O comando para modificar as permissões é `chmod`.

Para usar o comando chmod podemos atribuir permissões separadamente usando as letras `u` para o dono, `g` para o grupo e a letra `o` para os outros. Caso queira atribuir para todos basta usar a letra `a`.

Para adicionar uma permissão usamos o sinal de + enquanto para remover usamos o sinal -.

O formato do comando `chmod` é da seguinte maneira:

``` sh
chmod u+x nome_arquivo # adicionando permissão de execução para o dono do arquivo.
chmod g-r nome_arquivo # removendo permissão de leitura do arquivo.
chmod o+w nome_arquivo # adicionando permissão de escrita e deleção do arquivo para outros.
chmod a=rw nome_arquivo # definindo permissão de leitura, escrita e deleção para todos os users nesse arquivo.
```

### stick bit
Podemos adicionar stick bit nos diretórios usando o número 1 antes do octal das permissões. Quando adicionamos stickbit em um diretório somente o dono desse diretorio pode remover arquivos de dentro dele.

``` sh
chmod 1755 nome_do_diretorio/
```

O mesmo vale para atribuir permissões aos diretórios. Vale lembrar que para atribuir as permissões de maneira recursiva precisa-se colocar a flag `-R`.

## `chown`
O comando para modificar as permissões do dono do arquivo ou diretório `chown`.

``` sh
chown nome_do_user nome_do_arquivo
# ou podemos alterar user E grupo juntos...
chown nome_do_user:nome_do_grupo nome_do_arquivo
# ou para mudar somente o grupo do arquivo...
chown :nome_do_grupo nome_do_arquivo
```
Com esse comando o dono do arquivo será alterado.

Para atribuir permissões para o que há dentro de diretórios é necessário passar a flag `-R`.

## `chgrp`
O comando para alterar as permissões de um grupo de determinado arquivo ou diretório é `chgrp`.

``` sh
chgrp nome_do_grupo nome_do_arquivo
```

## SUID e SGID
Serve somente para arquivos binários. Caso tenha essa permissão, qualquer um pode executar o arquivo como se fosse dono dele (SUID) ou então como grupo dono do arquivo (SGID).

Um exemplo de binário que possui essa permissão é o comando su que se encontra em /bin/su.

## `umask`
Para definir um padrão de permissões para os arquivos usa-se o comando `umask`.

Essa definição funciona atraves de uma subtração do valor do umask pelos octais do chmod. Vejamos um exemplo.

O valor padrao que o Linux colocar para as permissões de arquivo é 0666 enquanto para diretórios é 0777.

``` sh 
# se o valor de umask for igual a 0002
# entao o valor padrao das permissoes sera
0666 - 0002 = 0664
# logo
chmod 0664 arquivo.txt
```
A mesma coisa funciona para diretorios.

Para alterar o umask fazemos
``` sh 
umask 0022
```

---

## Importante

Um diretório sem a permissão de execução (`x`) não é possivel entrar nele.

O stick bit é válido somente para diretórios.

*Quando um diretório possui stick bit somente o dono do arquivo pode alterar o arquivo!!!*
