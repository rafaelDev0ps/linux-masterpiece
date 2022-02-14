# Troubleshooting avancado
Apos realizar o teste basico de troubleshooting verificando processos (`top`), uso de memoria (`free`) e disco (`df -H`) podemos realizar testes de stress na maquina. Para isso podemos instalar a ferramenta `stress`.  
```console
$ sudo apt-get install stress
```  
  
Com essa ferramenta podemos definir os recursos utilizado pela maquina para realizar o teste de stress.  
```console
$ stress --cpu 3 --timeout 300s
```  
Veja que os processos do `stress` comecam a rodar na maquina.  
```console
PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+    COMMAND

17989 rafael    20   0    3856    100      0 R  50.0   0.0   0:27.07  stress

17990 rafael    20   0    3856    100      0 R  49.7   0.0   0:27.06  stress

1233 root       20   0       0      0      0 I   0.3   0.0   0:23.43  kworker:0-events

18115 rafael    20   0   13960   6036   4556 S   0.3   0.1   0:00.03  sshd

18126 rafael    20   0   11004   3756   3164 R   0.3   0.1   0:00.03  top
```  

Podemos testar o uso de memoria da maquina.  
```console
$ stress -m 200 --timeout 100s
```  
  
#### **IMPORTANTE**  
Quando um processo tenta usar 100% da memoria da maquina o kernel comeca a matar o processos que esta consumindo 100% da memoria, isso eh chamado de OOMKiller.  
```console
stress: FAIL: [18166] (415) <-- worker 18208 got signal 9
stress: WARN: [18166] (417) now reaping child worker processes
stress: FAIL: [18166] (415) <-- worker 18169 got signal 9
stress: WARN: [18166] (417) now reaping child worker processes
stress: FAIL: [18166] (415) <-- worker 18177 got signal 9
```  

### vmstat
Com a ferramenta `vmstat` podemos conferir o uso de memoria virtual da maquina.  
```console
$ vmstat

procs  -----------memory----------  ---swap-- -----io---- -system-- ------cpu-----
r  b   swpd    free   buff   cache   si   so    bi    bo   in   cs  us sy id wa st
0  0      0 4506988 140260 1302020    0    0    56   103   54  179   0  0 99  0  
```  
Nele eh informado o uso de memoria swap, I/O, cpu, etc. Para saber mais sobre o `vmstat` consulte o manual `man vmstat`.  
  
### iotop
Podemos fazer um `top` somente de processos que usam I/O no disco.  
```console
$ sudo apt-get install iotop

$ iotop
Total DISK READ:         0.00 B/s | Total DISK WRITE:         0.00 B/s
Current DISK READ:       0.00 B/s | Current DISK WRITE:       0.00 B/s
  TID  PRIO  USER     DISK READ  DISK WRITE  SWAPIN     IO>    COMMAND                                                           
    1 be/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % init maybe-ubiquity
    2 be/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % [kthreadd]
    3 be/0 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % [rcu_gp]
    4 be/0 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % [rcu_par_gp]
    6 be/0 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % [kworker/0:0H-kblockd]
    9 be/0 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % [mm_percpu_wq]
   10 be/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % [ksoftirqd/0]
   11 be/4 root        0.00 B/s    0.00 B/s  0.00 %  0.00 % [rcu_sched]
```  
Esse comando pode ser muito importante quando ha um banco de dados instalado no servidor ou uma aplicacao que consuma muito recursos em disco.  
  
### ifstat
Eh possivel verificar a performance de rede da maquina usando a ferramenta `ifstat`.  
```console
$ ifstat
      enp0s3      
 KB/s in  KB/s out
    0.23      0.38
    0.12      0.19
    0.12      0.19
    0.06      0.11
```  
Note que ele analisa a entrada e saida da interface de rede padrao. Eh possivel configurar a interface desejada usando a flag `-i`. Para mais informacoes dessa ferramenta veja `man ifstat`.  
  
### irqtop
Essa ferramenta permite que monitore as interrupcoes de hardware da maquina. Geralmente esse comando eh bastante util para maquinas que fazem grande consumo de rede, servidores movimentado, roteadores, etc.  
```console  
$ sudo apt-get install irqtop

$ irqtop
cobaia - irqtop - 2021-12-01 11:35:13 +0000
              CPU0
  cpuUtil:     2.0   total CPU utilization %
     %irq:     0.0   hardware IRQ CPU util%
    %sirq:     0.0   software IRQ CPU util%
 irqTotal:     104   total hardware IRQs
i      18:       5    IO-APIC  18-fasteoi   vmwgfx
i      19:       5    IO-APIC  19-fasteoi   ehci_hcd:usb1, enp0s3
i      21:       7    IO-APIC  21-fasteoi   ahci[0000:00:0d.0], snd_intel8x0
i     LOC:      84    Local timer interrupts
s   TIMER:      53
s  NET_RX:       5
s   BLOCK:       7
s TASKLET:       1
s     RCU:     108
```  
  
### iperf
Essa ferramenta eh usada para realizar testes de performance na rede entre dois pontos. 
```console
$ sudo apt-get install iperf

$ iperf

```