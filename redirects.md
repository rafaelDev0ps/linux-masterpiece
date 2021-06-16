# Redirecionadores

Os redirecionadores são compostos por file descriptors, cada um possui um valor:

## File descriptor (FD)
| FD | valor |
|---|---|
| stdin | 0 |
| stdout | 1 |
| stderr | 2 |

São usados da seguinte forma.

| comando | significado |   
|---|---|
| `>` | Redireciona a saida padrao (STDOUT) e sobrescreve |   
| `>>` | Redireciona a saida padrao e concatena com dados ja existentes |
| `<` | Redireciona a entrada padrao (STDIN) |   
| `<<` | Redirecionar entrada padrão concatenando |
| `2>` | Redirecionar uma saíde de erro |
| `2>>` | Redirecionar uma saíde de erro concatenando com algo já existente. |

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

Em saídas de erro usamos

``` sh
catjjj 2> erro.txt
```

Podemos redirecionar uma saída pertencente a outro file descriptor. Por exemplo:

``` sh
ls dir_nao_existente dir_existente > saida_erro.txt 2>&1
```

Nesse caso, o exemplo acima esta tratando o erro para ser observado pelo file descriptor 1 (STDOUT). E com isso tanto saídas de erro quanto saídas de sucesso serão gravadas.