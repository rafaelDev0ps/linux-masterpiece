máquinapadrãoé## Tarefas agendadas
Existem ferramentas no linux que nos permite agendar tarefas que serao executadas posteriormente.  
  
### Crontab
O `crontab` eh uma ferramenta que nos ajuda a definir qual tarefa executar repetidas vezes.  
```console
$ crontab -l   # lista cron jobs existente
$ crontab -e   # edita o arquivo de crontab
```  
  
No arquivo do crontab existe um padrao a ser seguido para que ele possa ser entendido corretamente.
```vim
minuto    hora    dia-do-mes    mes     dia-da-semana     user    comando
30  2  15  3  *   rafael    cat /var/log/meu-log.log
```  
No exemplo acima temos o comando `cat /var/log/meu-log.log` que sera executado pelo user `rafael` todo dia **15/03** as **2:30** de **qualquer dia da semana**.  
  
### at
O comando `at` diferente do `crontab` executa uma tarefa agendada apenas uma unica vez.  
```console
$ at 1:00
warning: commands will be executed using /bin/sh
at> echo "escrevendo no arquivo" > /tmp/opa
at> cat /tmp/opa<EOT>
job 1 at Fri Oct 29 01:00:00 2021
```  
No exemplo acima o comando at ira executar dois comando sequencialmente as 1:00 do dia 29 do outubro.  
  
Para listar os crons criados faca:  
```console
$ atq
1	Fri Oct 29 01:00:00 2021 a root
```
  
Para remover um cron criado pelo `at` faca:  
```console
$ atrm 1
```  
  
### batch  
Para ter maior seguranca ao realizar uma tarefa agendada podemos usar o `batch` que apenas executa as tarefas quando a maquina nao esta sendo sobrecarregada. Basta usar a palavra `batch` ao inves de `at`.  