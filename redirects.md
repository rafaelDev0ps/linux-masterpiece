# Redirecionadores

| comando | significado |   
|---|---|
| `>` | redireciona a saida padrao (STDOUT) e sobrescreve |   
| `>>` | redireciona a saida padrao e concatena com dados ja existentes |
| `<` | redireciona a entrada padrao (STDIN) |   
| `<<` |   |

É possivel criar arquivos com redirecionadores no Linux.

``` sh
cat ls > minha_saida.txt
```

É possivel escrever em um arquivo usando o redirecionador de entrada `<<`.

``` sh
cat << pinguim
> teste
> outro teste
> mais uma linha
> pinguim 
```

Note que pinguim é a palavra para definir o inicio e final da sentença.

Para criar um arquivo podemos juntar os redirecionadores.

``` sh
cat << pinguim > arquivo.txt
> teste
> outro teste
> agora estou criando um arquivo
> pinguim 
```

Por convenção usa-se a palavra EOF para definir o inicio e final de arquivo.