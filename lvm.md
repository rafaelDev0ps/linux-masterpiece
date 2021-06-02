# LVM - Local Volume Manager

Sistema de particionamento de disco dinamico, pode aumentar ou reduzir o teu particionamento sem precisar altera-lo.
Podemos vincular tanto uma partição quanto um HD no LVM.

Dispositivos fisicos (pendrive, redes e etc) são chamados de volumes fisicos no LVM. E essa parte não pode ser alterada.
Os volumes fisicos são associados a um grupo de volumes. Os grupos de volumes são atrelados aos volumes logicos.

Logo há 3 camadas:

 [Volumes fisicos]

 [Grupo de Volumes]

 [Volumes lógicos]


### PASSO A PASSO para criar um volume do tipo LVM

1° Definir as partições para o tipo Linux LVM
2° Criar volume fisico (através do comando pvcreate)
3° Criar um grupo de volumes (vgcreate)
4° Criar um volume lógico (lvcreate)

Com isso podemos perceber que o dispositivo criado no /dev é nosso grupo de volumes (assim como o sda, sdb...) seguido
pelo volume lógico que se refere as partições! Logo fica:

/dev/<grupo_volumes>/<volume_logico>

Não se perde performance quando usamos LVM. Pode haver um ganho de performance nas operações de gravação de blocos!


### COMANDOS
> wipefs -a <partição> = limpa a partição

> cfdisk <partição> = programa particionador

> partprobe <diretorio> = recarrega a tabela de partições

> pvcreate = cria volume físico (instalar pacote lvm2)

> pvdisplay ou pvs = mostra os volumes fisicos

> vgcreate <nome_grupo> <partição> = cria grupo de volumes

> vgdisplay ou vgs = lista grupo de volumes

> lvcreate = cria volume lógico

> lvextend -L +200M <volume> = altera o tamanaho do volume logico

> resize2fs = faz o resize do volume escolhido

> vgextend = expande o tamanho do grupo de volumes

> mount <partição> <diretorio> = monta volumes

> mkfs.ext4 <partição> = formata partição

> du -hs <diretorio> = verifica o volume ocupado pelo diretorio

> lsblk = lista volumes em formato de arvore


### DICAS
- Não precisa criar uma partição muito grande logo de inicio, é possivel utilizar o lvextend e resize2fs (um seguido do outro) para ir aumentando o volume aos poucos.



### DUVIDAS FREQUENTES
P: Para utilizar mais de 16Tb de capacidade no armazenamento do ext4, que opção é essencial no mke2fs.conf?

R: 64bit


P: Caso ao usar o mkswap receba a mensagem 'file has holes'?

R: O arquivo de swap foi criado usando um arquivo Copy-on-Write, que não aloca espaço no momento da criação.


P: O comando reset faz?

R: reinicia o terminal, corrigindo os caracteres


P: Para ganhar mais performance para listar os pontos de montagem?

R: Vá a fonte dando /proc/mounts


P: É possível criar Swap em uma VPS que somente possui disco com todo espaço particionado como / ?

R: Verdadeiro


P: Em um LVM, a partição de disco física é corresponde ao...

R: Volume físico
