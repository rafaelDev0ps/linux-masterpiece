## Como configurar um servidor web?
Primeiro, podemos perguntar qual a finalidade desse servidor? Um e-commerce ou um sistema de gerenciamento de gualpao de uma loja pequena?  
Segundo, quanto de espaco em disco necessario para essa aplicacao?  
Terceiro, qual sera o crescimento desse sistema? Vai ser desativado no futuro? Vai ser um servidor que ira arquivar os logs de uma empresa?  
  
## Como calcular o tamanho ideal inicial do disco?
Tamanho total, tipo, crescimento do que sera hospedado (site, db, logs), usar LVM.  
  
Tipos de disco:
- SATA 350 Mb/s
- SSD 600 Mb/s
- Flash 50Mb/s
- NVME/M2 6Gb/s
- SAS 450Mb/s
  
## Requisitos de Memoria
Quando possuimos muitos acessos simultaneos, quanto mais memoria disponivel, melhor sera o desempenho.
  
- Java: necessario 4Gb
- dnsmasq: necessario 1Mb
- bind: 50 Mb
- dhcp: 10 Mb
- Apache: 20 Mb
  
## CPU
Frequencia da CPU, cache L2, tipo de operacao.  
- Residencial: AMD Rysen 7, Intel i3, i5, i7, i9 ...
- Enterprise: Intel Xeon, AMD EPYC
  
## Rede de Comunicacao
Velocidade, Tecnologia, distancia e hospedagem.  
- Velocidade (10/100/1000/10Gb/100Gb)
- Tecnologia: cabeada, fibra, virtual switch
- distancia (+distancia +latencia)
- hospedagem internacional eh sempre mais barata
