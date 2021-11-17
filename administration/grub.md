# GRUB (Grand Unified Bootloader)
O GRUB é responsável por realizar o boot do sistema operacional. Ele fica localizado no volume MBR da máquina.  
  
A função do GRUB é gerenciar o boot do sistema. Ele faz isso montando o kernel do Linux na memória e inicia o processo chamado `init 1`.  
Podemos ver os arquivos responsáveis por essa inicialização no diretório `/etc/grub.d`. Dentro desse diretório encontraremos os seguintes scripts shell.  
```bash
-rwxr-xr-x 1 root root 10627 jan 13  2021 00_header
-rwxr-xr-x 1 root root  6258 jan 13  2021 05_debian_theme
-rwxr-xr-x 1 root root 18151 ago 12 06:18 10_linux
-rwxr-xr-x 1 root root 42359 jan 13  2021 10_linux_zfs
-rwxr-xr-x 1 root root 12894 jan 13  2021 20_linux_xen
-rwxr-xr-x 1 root root  1992 ago 18  2020 20_memtest86+
-rwxr-xr-x 1 root root 12059 jan 13  2021 30_os-prober
-rwxr-xr-x 1 root root  1424 jan 13  2021 30_uefi-firmware
-rwxr-xr-x 1 root root   214 jan 13  2021 40_custom
-rwxr-xr-x 1 root root   216 jan 13  2021 41_custom
-rw-r--r-- 1 root root   483 jan 13  2021 README
```  
Esse arquivos são executados em ordem (como estão listados) e cada um tem uma responsabilidade. Caso queira alterar alguma configuração do GRUB é indicado editar os arquivos `40_custom` e/ou `41_custom`.  
  
Podemos encontrar o kernel do linux no diretório `/boot` da máquina no arquivo `/boot/vmlinuz`. Outro arquivo que será utilizado durante o boot será o `/boot/initrd.img`.  
  
Os arquivos encontrados em `/etc/grub.d` geram dinâmicamente um arquivo de configurações do GRUB em `/boot/grub/grub.cfg`.  

### Editando GRUB
Para editar o GRUB é necessário editar o arquivo `/etc/default/grub`, nesse arquivo você pode customizar seu GRUB. Para que as alterações sejam salvas você precisa executar o comando `update-grub`.  
  
### Recuperando o sistema
Caso tenha acontecido algo errado com a inicialização impedindo que consiga entrar no sistema é possível recorrer ao modo linha de comando do GRUB.  
Quando inicializar o GRUB digite `c` para entrar no CLI do GRUB. após isso tente encontrar em qual dispositivo está instalado o Linux. Podemos fazer isso através do comando `ls`.  
Após descobrir em qual partição está seu Linux execute o comando `set`.  
```sh
set prefix=(hd0,msdos2)/boot/grub
```  
Agora precisamos dizer que esse diretório será o padrão para fazer o boot do Linux.  
```sh
set root=(hd0,msdos2)
```  
  
Por último executamos o comando `insmod`.  
```sh
insmod linux
insmod normal
normal
```  
  
### Caso tenha problemas com o carregamento do kernel
Se houver problemas no carregamento do kernel podemos defini-lo pelo CLI do GRUB também.  
```sh
set root=(hd0,msdos2)
linux /boot/vmlinuz-5.11.0-00-generic root=/dev/sda1
```  
A mesma coisa server para o script `initrd` passando como parâmetro o caminho do arquivo.  
  
Após isso digite `boot` no GRUB CLI para inicializar o sistema operacional.  