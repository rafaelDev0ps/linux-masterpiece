você# VI (Visual Interface)

Para instalar o VIM use
``` sh
sudo apt-get install vim
```

## Inserindo texto
Ao aperta `ESC` ira retornar ao modo comando.

Para inserir texto aperte a letra `i`. Aparecera `--- INSERT ---`. Se usarmos `I` iremos inserir texto no inicio da linha onde esta o cursor.

Para inserir na linha de baixo basta apertar `o`. Para inserir na linha de cima usa-se `O`

Se usermos `a` ira iniciar o modo de insercao um caractere a frente. Se usar `A` ira inserir um caractere no final da linha.

## Salvando e saindo
| comando | significado |
| --- | --- |
| `:w` | salva |
| `:q` | sair |
| `:q!` | sair sem salvar |
| `:wq` ou `:x` | sair e salvar |
| `Shift`+`ZZ` | sair e salvar |
| `Shift`+`ZQ` | sair sem salvar |

## Copiar e colar texto
Para copiar uma linha usa-se no modo comando `yy`.

Para colar a linha usa-se no modo comando `p`. Ja `P` copia na linha a baixo.

Para copia mais de uma linha usamos `y<numero-de-linhas>y`.

Se usarmos `r` podemos substituir o caractere. Basta digitar `r` + `caractere novo`.

## Remover texto
Para apagar uma linha inteira usa-se `dd` no modo comando.

Para recortar texto fazemos primeiro `dd` depois `p` na linha desejada.

Para remover mais de uma linha usamos `d<numero-de-linhas>d`.

Para remover apenas um caractere usa-se `x`. Ja o `X` apaga um caractere antes do cursor.

Para desfazer as alteracoes no arquivo basta digitar na linha de comando `u` e para refazer usa-se `Ctrl`+`r`.

Podemos remover o resto do arquivo a partir de um ponto inicial usando `dG` para remover o resto que esta abaixo da linha. Ou podemos usar `dgg` para remover o resto que esta acima da linha.

## Alterar texto
Para alterar uma palavra ou senteça da linha basta digitar no modo comando:
``` vim
:<numero-linha>s/<palavra-atual>/<nova-palavra>/
```

Para todo o arquivo fazemos:
``` vim
%s/<palavra-atual>/<nova-palavra>/
```

## Modo Visual
Ao digitar `v` no modo comando entramos no modo visual.

O modo visual permite selecionar um pedaco do texto de uma ou mais linhas usando `Shift` + `direcional`.

## Modo Visual Block
Ao digitar `Ctrl` + `v` no modo comando entramos no modo visual block.

O modo visual block faz a selecao de linhas verticalmente, facilitando a manipulacao de mais de uma linha.

## Busca
Para buscar uma palavra ou sentença basta digitar `/` no modo comando seguido da palavra desejada.Quando apertar `n` (next) ele vai para proxima palavra na busca (se existir).

Caso queira fazer uma busca ascendente use `?` no modo comando segjuido da palavra desejada. Se apertar `N` (maiúsculo) ele vai para a proxima palavra de cima.

## Posições
Para ir no final do arquivo digite `G` no modo comando. E para o início da linha digite `gg`.

Existem outros comandos como 
- `H` topo da tela
- `M` meio da tela
- `L` final da tela

## Configurações
No modo comando:
- `:set number` numeração de linha
- `:set hlsearch` highlight em buscas
- `:set tabstop=2` tamanho do TAB medido em espaços
- `:set expandtab` converte o TAB em espaços
- `:set noerrorbells` silencia barulhos de erro
- `:set novisualbells` silencia barulhos no modo visual
- `:syntax=on` reconhece sintaxe da linguagem do arquivo

Caso queira customizar o VIM basta alterar o arquivo `.vimrc`.

## Arquivos
Para abrir arquivos sem sair do VIM basta digitar `:e /caminho/do/arquivo`.

Para dividir a tela com outro arquivo usamos o `:split <nome do arquivo>` ou `:vsplit do arquivo`

Se usarmos o `:qa` sairemos de todos os arquivos abertos.

## Comandos linux dentro do VIM

Basta digitar `:! comando` para executar um comando no bash sem sair do VIM.

Ou caso queira a saída do comando no arquivo no VIM basta usar `:.! comando`.

## Importante
Toda vez que voce deleta uma linha o VIM guarda essa remocao em buffer caso queira utiliza-la psteriormente.