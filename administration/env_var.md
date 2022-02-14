sãoé# Variaveis de Ambiente

Uma variavel de ambiente nada mais e um campo da memoria que eh reservado. Existem varias variaveis de ambiente no Linux, grande parte delas sao usadas pelos programas instalados.

``` sh
# lista as variaveis
printenv
env

# criar variaveis
NOME_VARIAVEL=valor_da_variavel
export NOME_VARIAVEL=valor_da_variavel
set NOME_VARIAVEL=valor_da_variavel

# desfazer variavel criada
unset $NOME_VARIAVEL
```

Se uma variavel possuir mais de um valor eh necessario separa-los com `:`.

``` sh
export MINHA_VAR=valor1:valor2
```

## `alias`

Serve para rotular comandos

``` sh
alias k=kubectl

unalias k # desfazendo bind
```
