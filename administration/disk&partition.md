sãomáquinavocêapósé## Como verificar discos e particoes
Para fazer a listagem dos discos podemos usar o comando `fdisk`.  
```sh
Device         Boot  Start      End  Sectors  Size Id Type
/dev/mmcblk0p1 *      2048   526335   524288  256M  c W95 FAT32 (LBA)
/dev/mmcblk0p2      526336 60620766 60094431 28.7G 83 Linux
```  
  
### Caso um novo disco seja adicionado na maquina...
Se um novo disco for adicionado na maquina o primeiro passo eh criar a(s) particao(oes) no novo disco. Para isso usamos a ferramenta `cfdisk`.  
Apos criar as particoes eh necessario anexar o filesystem na particao. Para isso usamos o seguinte comando.  
```sh
$ mkfs.ext4 /dev/sdc1
```  
No exemplo acima a nova particao esta em `/dev/sdc1`.  
  
Em seguida, monte seu volume em um diretorio desejado.  
```sh
$ mkdir ~/meu-novo-volume
$ mount -t ext4 /dev/sdc1 ~/meu-novo-volume  
```  
Caso deseje, voce pode persistir esse mount editando o arquivo `/etc/fstab`.  
  
## Como verificar a integridade de disco
Usamos o comando `fsck` para verificar a integridade do disco. Para que essa verificacao funcione eh necessario desmontar o disco pois corre o risco de corromper os arquivos que nele existem.  
```sh
$ umount /dev/sdc1
$ fsck /dev/sdc1
```  
  
Alem disso podemos configurar para que seja feita uma verificacao na particao a cada determinado periodo. Fazemos isso atraves da ferramenta `tune2fs`.  
```sh
$ tune2fs -i w /dev/sda2

tune2fs 1.45.5 (07-Jan-2020)
Setting interval between checks to 0 seconds
```  
Acima esta sendo configurado para que a verificacao ocorra semanalmente. Verifique mais possibilidades em `tune2fs --help`.  

## **Dica**
Para que seja feito a verificacao do sistema de arquivos no boot eh necessario alterar as configuracoes do seu gerenciador de boot. Caso esteja usando o GRUB como gerenciador de boot edite o arquivo `etc/default/grub`.  
```cfg
GRUB_CMDLINE_LINUX_DEFAULT="quiet fsck.mode=force"
```  
```sh
$ update-grub
```  
  
## Badblocks
Badblocks sao setores de disco defeituosos onde o sistema operacional eh incapaz de escrever. Podemos verificar se ha badblocks no device usando o comando `badblocks`.  
```sh
$ badblocks -nsv -c 1024 /dev/sdb1

Checking for bad blocks in non-destructive read-write mode
From block 0 to 1047534
Checking for bad blocks (non-destructive read-write test)
Testing with random pattern: done                                                 
Pass completed, 0 bad blocks found. (0/0/0 errors)
```  
Para saber mais sobre o comando `badblocks` use `badblocks --help`.  