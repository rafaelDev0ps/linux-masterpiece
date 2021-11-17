## Entendendo IPs
São compostos por 4 octetos (2^8 = 256). Ou seja:

``` sh
# em binário
11111111 . 11111111 . 11111111 . 11111111

# em decimal
255 . 255 . 255 . 255
```

A mascara da rede (Netmask) define os limites do endereco de rede e do host. Por exemplo:

``` sh
# se netmask for 255.255.255.0
# o a rede sera definida nos 3 primeiros octetos
# o ip dos hosts serao definidos no ultimo octeto
```

## Classes de IP
A classe eh determinada pela mascara.
  
Classe A  
Netmask: 255.0.0.0  
Quantidade de IPs: 16.777.214  
  
Classe B  
Netmask: 255.255.0.0  
Quantidade de IPs: 65.534  
  
Classe C  
Netmask: 255.255.255.0  
Quantidade de IPs: 256  

## CIDR
Eh a quantidade de bits que sua mascara esta usando. Usa-se a seguinte notacao:  

`192.168.70.37/24`  

Logo podemos dizer que a mascara do IP `192.168.70.37` possui 24 bits ou seja `255.255.255.0`.  
Atraves do CIDR podemos descobrir a mascara.
