# Administracao de Usuarios

O comando para adicionar users e ```adduser```
Esse comando tem um arquivo de configuracao em /etc/adduser.conf

> ```id``` ou ```id nome-do-user``` = mostra o id do usuario, grupo do usuario 

> ```cat /etc/groups = arquivo que salva os grupos.```

No diretorio /etc/skel ficam as configuracoes default usada na criacao de cada usuario. Assim que os usuarios sao criados os arquivos
que estao dentro de /etc/skel sao copiados para a pasta do usuario.

Para criar um user admin basta colocar ele no mesmo grupo do user root de valor 0.

> ```adduser --gid 0 newroot```

Podemos criar users atraves do comando `useradd`

> ```useradd -u 3434 -g 0 -s /bin/zsh rafael```

A diferenca entre o comando adduser e useradd é que em `adduser` as configuracoes de criacao estao em /etc/adduser.conf enquanto
no comando `useradd` as configuracoes do usuario devem ser criadas apos sua criacao.

O arquivo de configuracao dos usuarios se encontra em /etc/passwd. O arquivo e separado em linhas e colunas separadas por ':'.

[username] : [senha] : [uid] : [gid] : [nome] : [role] : [telefone] : [telefone-trabalho] : [diretorio] : [shell]

A senha fica no arquivo /etc/shadow. Nesse arquivo as senhas estarao criptografadas. Caso no lugar da senha tenha um caractere '!' significa que o usuario nao possui senha definida. Se tiver o caracter '\*' significa que o arquivo nao tem direito de mostrar a senha.

Podemos remover um usuario usamos o comando `deluser` ou `userdel`

> ```deluser --remove-home girus```

Para criar um grupo de users usamos o comando `groupadd` ou `addgroup`.

> ```groupadd novogrupcato```

> ```adduser --group novogrupo``` (tambem é possivel atraves de adduser) 

O arquivo onde os grupos ficam salvos esta em /etc/groups. E o arquivo de configuracoes é o mesmo de `adduser`.
Para identificar um grupo de sistemas o gid deve estar entre 100 e 999.

Os arquivos relacionados aos grupos sao /etc/group e /etc/gshadow. Eles possuem a mesma formatacao que osarquivos relacionados aos usuarios.

Para remover um grupo usamos o comando `delgroup` ou `groupdel`:

> ```delgroup nome-grupo```

> ```groupdel nome-grupo```


Para definir a senha de um user usamos o comando `passwd`:

> ```passwd nome-do-user```

Podemos barrar a autenticacao do user passando a flag `-l` ou `--lock`.

Para expirar a senha do user basta passar a flag `-e`.

Para deletar a senha do user usamos `-d`.


Para mudar de user basta usar o comando `su`:

> ```su - nome-do-user```

### Importante
O user id do usuario admin sera sempre 0.
Se quiser remover um grupo primario sera necessario remover os usuarios desse grupo primeiro.


### Siglas
GID = group id.

UID = user id.
