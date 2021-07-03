# Logs
Log é um arquivo que registra um evento ocorrido no sistema operacional.

Podemos encontrar os logs (por padrão) no diretorio `/var/log`.

## Logs do sistema
Para podermos configurar os logs do sistema podemos olhar atraves do arquivo /etc/rsyslog.conf.

Sobre o arquivo `/etc/rsyslog.conf`, existem regras para que os logs sejam salvos que sao organizados da seguinte maneira.

`facilidade`.`nivel`\t `caminho_do_arquivo.log`

Podemos interpretar essa configuracao da seguinte forma: "todos os logs dessa facilidade de nivel X serao guardados no arquivo `caminho_do_arquivo.log`".

Exemplo:

``` vim
kern.err    /var/log/erros_sistema.log
```
Ou seja, os logs do `kernel` que sejam ATÉ o "tipo" `err` serao gravados no arquivo `/var/logs/erros_sistema.log`.

Para saber mais sobre cada facilidade e nivel do sistema basta consultar o site Guia Foca na secao de Logs.

Caso queira somente mensagens de um determinado tipo devemos fazer:

``` vim
kern.=err /var/log/erros_sistema.log
```

Nesse caso somente mensagens do tipo `err` serao gravadas no arquivo.

## Como criar um servidor de logs atraves do `rsyslog`?
No arquivo `/etc/rsyslog.conf` sera necessario configurar as seguintes linhas abaixo. 

``` vim
#################
#### MODULES ####
#################

module(load="imuxsock") # provides support for local system logging
#module(load="immark")  # provides --MARK-- message capability

# provides UDP syslog reception
module(load="imudp")
input(type="imudp" port="514")

# provides TCP syslog reception
module(load="imtcp")
input(type="imtcp" port="514")

# O endereco do meu servidor de log eh 192.168.74.50
auth.*  @192.168.74.50
```

Para apontar os logs de um cliente para um servidor remoto basta usar o `@<ip-do-servidor>`.

## Gerenciamento de Logs
Podemos gerenciar os arquivos de logs atraves do `/etc/logrotate` e `/etc/logrotate.d/`.

Para testar sua configuração de logrotate é necessário forçar a rotação usando o seguinte comando.

``` sh
logrotate -f /etc/logrotate.conf
```

Dentro do diretorio `/etc/logrotate.d/` temos as configuracoes de log dos demais programas e arquivos.

``` vim 
/var/log/apt/meu-arquivo.log {
  rotate 12
  monthly
  compress
  missingok
  notifempty
}

```

## JOURNALCTL
Podemos analisar os logs atraves do comando `journalctl`

``` sh
journalctl --utc # logs no tempoformato UTC
journalctl -b # logs de boot
journalctl -b --since "2021-07-03" # logs a partir de uma data
journalctl -b --since "2021-07-03 07:30" --until "2021-07-04 07:30" # logs de um periodo de tempo
journalctl --since today --until "6 hours ago"
journalctl -u cron # especifica o logs de um servico especifico
journalctl -k -p err # passando nivel do log (err, debug, info, emerg, alert, crit, notsee, warn)
journalctl -b -o json # especifica o formato do output (short, json, json-pretty, short-iso) 
```

Alem do comando acima existe o arquivo onde podemos configurar o jounaling `/etc/systemd/journald.conf`.

## DICA
É extremamente recomendado ter uma maquina remota exlcusiva para logs do servidor de uma maneira segura.

## Fonte sobre log
(Guia Foca Logs)[https://www.guiafoca.org/guiaonline/intermediario/ch17s02.html]

