sãomáquinavocêresponsável# O Kernel
O nucleo do SO, faz o controle dos recursos da maquina e responsavel por fazer ponte entre o usuario e o hardware.  
   
No Linux tambem existem drivers, sao chamados de modulos.  
Para listar os modulos instalados na maquina fazemos:  
```sh
lsmod
```  
Atraves do `udev` o Linux pode carregar os modulos necessarios para o programa que voce deseja usar.  
Podemos ver a versao do kernel atraves do comando `uname -a`.  
  
Para termos acesso aos firmwares instalados na maquina precisamos ir ate o diretorio `/lib/firmware`.  
