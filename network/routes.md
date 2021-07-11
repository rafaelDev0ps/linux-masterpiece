## Rotas Calculo Mascara

Uma rota eh o caminho que o pacote faz para chegar ao destino desejado.  
``` sh
ip route ls # lista as rotas atuais
```
  
Podemos instalar uma ferramenta para calculo de mascaras ao inves de fazer o calculo na mao.
``` sh
apt-get install subnetcalc
```
  
Para usar fazemos:  
```sh
$ subnetcalc 192.168.1.0/24

Address       = 192.168.1.0
                   11000000 . 10101000 . 00000001 . 00000000
Network       = 192.168.1.0 / 24
Netmask       = 255.255.255.0
Broadcast     = 192.168.1.255
Wildcard Mask = 0.0.0.255
Hosts Bits    = 8
Max. Hosts    = 254   (2^8 - 2)
Host Range    = { 192.168.1.1 - 192.168.1.254 }
Properties    =
   - 192.168.1.0 is a NETWORK address
   - Class C
   - Private
GeoIP Country = Unknown (??)
DNS Hostname  = (Name or service not known)
```
  
## Multiplas redes
_Como podemos conectar com hosts de outras redes?_  
  
Podemos adicionar a rede na interface da placa *caso estejam na mesma rede fisica e o host seja conhecido*.  
```sh
id addr add 192.168.2.1/24 # a nova rede conhecida eh 192.168.2.2/24
```
  
Podemos remover uma rota criada fazendo:  
```sh
ip route del 192.168.2.1/24
```
  
O roteamento eh separado do enderecamento de IP, um nao funciona sem o outro.  

## Gateway
Para fazer um roteamento tipo gateway eh necessario passar um segundo host que ficara entre os dois endpoints.  
```sh
ip route add 192.168.1.32/24 via 192.168.1.22
```
  
Nesse caso ele vai fazer as chamadas para 192.168.1.22 onde sera encaminhado para 192.168.1.32.  
Para que a maquina local consiga alcancar os demais destinos eh necessario ter configurado uma interface gateway padrao.  
Todas os pacotes antes de sairem para a rota definida passam pelo gateway padrao.  
  
Para adicionar o gateway padrao fazemos:  
```sh
ip route add default via 192.168.1.1
```

_Eh possivel adicionar mais de um gateway padrao?_  

Por padrao a metrica de rotas para gateway eh sempre zero. Porem podemos adicionar uma rota de gateway padrao fazendo:  
```sh
ip route add default via 192.168.2.1 metric 1
```  
  
Com isso iram existir mais um gateway padrao. Um com a metrica 0 e outro com metrica 1. Como temos rotas semelhantes a metrica com o menor numero tera mais chance de ser escolhida.  
  
Com isso podemos fazer um sistema de redundancia caso haja algum problema com uma maquina do servidor os pacotes irao ser enviados pelo outro gateway padrao.  
  
## Interfaces hotplug
Podemos configurar nossas interfaces de rede no arquivo `/etc/network/interfaces`.

```vim
auto lo # o auto significa que ele vai levantar a placa de rede durante o boot
iface lo inet loopback

auto enpos3
iface enp0s3 inet static # essencial para servidores publicos
  address 192.168.1.22/24
  gateway 192.168.1.6
```  
  
Para configurar interface cliente DHCP fazemos

```vim
iface enp0s3 inet dhcp # essencial para servidores publicos
  address 192.168.1.22/24
  gateway 192.168.1.6
```   
  
Para habilitar o hotplug fazemos:  
```vim
# auto enpos3 # nao configura a placa enp0s3 automaticamente
allow-hotplug # levanta a placa de rede se houver um link conectado e funcional na maquina
```  
  
Dessa maneira permitimos que o processo de redundancia de hosts funcione, pois assim que um link de conexao cair ele ira remover a interface antiga e aplicar a nova interface que possui uma conexao funcional (confiurando gateway padrao e rota).  
  
Para terminar com um link de conexao na interface basta usar o comando `ifdown` e para criar uma conexao com a interface usamos `ifup`.  
``` sh
ifdown enp0s3 # termina a conexao do link
ifup enp0s3 # levanta a conexao do link
```
  
O processo responsavel por cuidar da troca do IP da maquina e o `dhclient`
  
## Importante
Organize sua lista de rotas de uma maneira simples para voce consiga dar manutencao depois. Segregue as rotas para contextos diferentes.  
Para conseguir alcancar o destino eh necessario criar a rota E o ip do host.  

Para saber quais interfaces de rede a maquina possui podemos usar o comando `ip link`.  
```sh
ip link ls
```
