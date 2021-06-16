# Onde pedir ajuda no Linux?

Podemos usar as páginas dos manuais.

``` sh
# basta digitar man <nome-do-comando>
man ls
man cat
```

Podemos encontrar os arquivos do man no diretorio `/usr/share/man`.

O man é separado por sessoes, cada uma delas corresponde a um grupo especifico de comandos.

Os diretorios diretorios do man possui vários arquivos compactados que quando voce busca por um comando ele descompacta o arquivo e mostra no terminal.

Se o comando estiver em mais de uma sessão voce pode escolher a sessão colocando o numero da sessão desejada.

``` sh
man 3 <nome-do-comando>
# por padrão o man mostra sempre a primeira sessão desse comando
```

Para saber se existe mais de uma sessao do comando podemos passar o argumento `-k` no comando do man.

## `--help`

Grande parte dos comando linux possui uma flag chamada --help que te ajuda a usar o comando desejado.

``` sh
cat --help
ls --help
# ou
help cat
help ls
```

## `apropos`

Podemos usar o comando `apropos` para obter o indice dos comandos.

``` sh
apropos cat
apropos ifconfig
apropos -w i?config # passando a flag -w temos a opção de fazer uma busca
```

## `whatis`

Aprensenta o significado do comando de uma maneira mais resumida.

``` sh
whatis cat
```

## `which`

Mostra o caminho para o binario do comando.

``` sh
which cat
```

## Sites

[The Linux Documentation Project](tldp.org) DESATUALIZADO
[Guia Foca](guiafoca.org)


## YouTube
[LINUXTips](https://www.youtube.com/user/linuxtipscanal)