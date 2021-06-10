# Administracao de Grupos e Usuários

## Users

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

Para modificar os dados de um user usamos o comando `usermod`. Podemos modificar tudo de um user desde o uid até os comentários do user.

Podemos usar o comando `chfn` (change full name) para alterar informações do usuário também. Assim como o `chfn` temos o `chsh` para mudar o shell do usuário.

Para definir a senha de um user usamos o comando `passwd`:

> ```passwd nome-do-user```

Podemos barrar a autenticacao do user passando a flag `-l` ou `--lock`.

Para expirar a senha do user basta passar a flag `-e`.

Para deletar a senha do user usamos `-d`.


## Grupos

Para criar um grupo de users usamos o comando `groupadd` ou `addgroup`.

> ```groupadd novogrupcato```

> ```adduser --group novogrupo``` (tambem é possivel atraves de adduser) 

O arquivo onde os grupos ficam salvos esta em /etc/groups. E o arquivo de configuracoes é o mesmo de `adduser`.
Para identificar um grupo de sistemas o gid deve estar entre 100 e 999.

Os arquivos relacionados aos grupos sao /etc/group e /etc/gshadow. Eles possuem a mesma formatacao que osarquivos relacionados aos usuarios.

Para remover um grupo usamos o comando `delgroup` ou `groupdel`:

> ```delgroup nome-grupo```

> ```groupdel nome-grupo```

Assim como nos usuários podemos alterar as informações de grupos já criados usando o comando `groupmod`.

Para definir a senha para um grupo usamos o comando `gpasswd`:

> ```gpasswd nome-do-grupo```

Para adicionar um user a um grupo criado usamos a flag `-a` do comando `gpasswd`:

> ```gpasswd -a nome-do-user nome-do-grupo```

Para adicionar um administrador de um grupo usamos a flag `-A` do comando `gpasswd`:

> ```gpasswd -A nome-do-user nome-do-grupo```

Para adicionar um usuário em um grupo somente durante uma sessão usamos o comando `newgrp -`.

Podemos verificar se um user é admin de um grupo olhando o arquivo /etc/gshadow. O arquivo tem a seguinte formatação:

[nome-grupo] : [hash-senha] : [nome-admin] : [nome-users]

Para remover um usuário de um grupo usamos a flag `-d` do comando `gpasswd`:

> ```gpasswd -d nome-do-user nome-do-grupo```


## Bonus

Para mudar de user basta usar o comando `su`:

> ```su - nome-do-user```

Podemos ver os últimos logins dos usuários chamado `lastlog`, que utiliza o arquivo /var/log/lastlog.

### Importante
O user id do usuario admin sera sempre 0.
Se quiser remover um grupo primario sera necessario remover os usuarios desse grupo primeiro.


### Siglas
GID = group id.

UID = user id.
