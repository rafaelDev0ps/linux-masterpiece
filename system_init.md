# SystemV e SystemD
A inicialização do Linux acontece primeiramente com a verificação do BIOS, após isso acontece uma consulta no disco para encontrar o MBR e o GRUB.  
Após selecionar o Linux no GRUB acontece o carregamento do kernel onde é chamado o processo de init que é responsavel de subir as demais coisas (rede, UI, etc).  
Atualmente o processo responsavel por isso é o SystemD, antigamente era usado o SystemV.  
  
## SystemV
Podemos configurar o systemV através do arquivo `/etc/inittab`. Existem varios tipos de inicializacao do sistema que sao separados por numeros, vejamos:  
- `0` halt
- `1` single-user
- `2-5` multi-user
- `6` reboot
  
Podemos encontrar mais sobre a configuracao do SystemV [aqui](https://manpages.debian.org/jessie/sysvinit-core/inittab.5.en.html).  
  
## SystemD
Atualmente o SystemD eesta sendo usado no lugar do SystemV. Nele, ao inves de termos runlevels temos targets, que sao chamados pelo sistema na inicializacao.  
Para realizar operacoes no SystemD usamos o comando `systemctl`.  
Alguns comandos com a mesma funcionalidade do SystemV sao:  
- `systemctl isolate rescue` halt
- `systemctl isolate multi-user.target` multi-user
- `systemctl isolate graphical.target` interface grafica
- `systemctl get-default` visualiza runlevel padrao
- `systemctl set-default multi-user.target` define  runlevel padrao
  
No diretorio `/etc/systemd/system` encontramos as definicoes de como os servicos instalados na maquina devem ser inicializados.
  
Para verificar se um servico esta ativo usamos o comando  
```sh
systemctl is-active sshd
```
    
## Importante
Para verificar em qual runlevel a maquina esta basta utilizar o comando `runlevel`. 
