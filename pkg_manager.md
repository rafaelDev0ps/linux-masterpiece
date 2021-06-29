# Gerenciadores de Pacote

Para descobrir qual é sua distribuição basta verificar o arquivo issue.
``` sh
cat /etc/issue
```

Com base na distribuição podemos saber qual gerenciador de pacotes padrão. Conforme a tabela:
| Distribuição | PKG Manager |
| --- | --- |
| Debian | dpkg e apt |
|  |  |

## Diferença entre dpkg & apt
A diferença entre o dpkg e apt é que no dpkg o pacote com extensão `.deb` além disso ele não resolve dependências. Já o apt consegue fazer o download do pacote buscando nos repositórios conhecidos pela sua máquina e consegue resolver as dependências do pacote.

Porém quando o apt baixa o pacote com as dependêcias quem realiza a instalação é o dpkg.

## Debian Package (dpkg)
Para fazer uma instalação pelo dpkg fazemos:
``` sh 
dpkg -i nome-do-pacote.deb
```

Para listar os pacotes
``` sh
dpkg -l
```

Para remover os pacotes
``` sh
dpkg -r nome-do-pacote
# ou
dpkg -P nome-do-pacote
```

Para encontrar os arquivos que fazem parte de um pacote
``` sh
dpkg -L nome-do-pacote
```

Para saber mais sobre determinado pacote 
``` sh
dpkg -I nome-do-pacote
```

Para verificar se há um problema no pacote
``` sh
dpkg -C nome-do-pacote
```

## Aptitude (apt)
Utiliza uma lista de repositórios para o dpkg instalar o pacote desejado.

``` sh
apt-get install <nome-do-pacote> # instala pacote
apt-get update # atualiza a lista de repositórios
apt-get purge <nome-do-pacote> # remove pacote à força
apt-get auto-remove # remove pacotes inutilizados
apt-get upgrade # atualiza toda a distribuição
apt-key add <chave> # verifica chave do repositório desejado
apt-get clean # limpa arquivos deb usados pela instalação
```

A lista de repositório se localiza no diretório `/etc/apt/source.list`. Os repositórios que não fazem parte da distribuição devem ser colocados no diretório `/etc/apt/source.list.d`.

Os arquivos baixados e instalados pelo apt são salvos no diretório `/var/cache/apt/archives`
