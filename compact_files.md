## Compactadores de arquivos
  
### TAR
```sh
tar -cvf /caminho/do/meu/arquivo.tar /caminho/dos/arquivos/compactados
```  
  
### Compactadores
``` sh
sudo apt-get install gzip
sudo apt-get install bzip2  #ideal para arquivos texto
sudo apt-get install xz  # bom para binarios
```  
Para compactar arquivos `bzip` fazemos:  
```sh
tar -cvjf /caminho/do/meu/arquivo.bz2 /caminho/dos/arquivos/compactados
```

Para compactar arquivos `xz` fazemos:  
```sh
tar -cvJf /caminho/do/meu/arquivo.tar.xz /caminho/dos/arquivos/compactados
```
Para compactar arquivos `gzip` fazemos:  
```sh
tar -cvzf /caminho/do/meu/arquivo.tar.gz /caminho/dos/arquivos/compactados
```  

### ZIP
```sh
sudo pat-get install zip unzip
```  
  
Para compactar:  
```sh
zip -c /caminho/do/meu/arquivo.zip /caminho/arquivos/compactados
unzip -c /caminho/do/meu/arquivo.zip /caminho/arquivos/compactados
```  
