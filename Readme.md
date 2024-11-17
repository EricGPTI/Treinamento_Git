### Listando GPG Keys existentes
gpg --list-secret-key --keyid-form LONG

Este comando permite que, caso exista uma chave GPG, você pegue o ID da chave para configurações posteriores.

### Gerando GPG Key
gpg --full-generate-key

Após isso é só seguir o passo a passo.
Com a chave gerada é hora de utilizar a chave para assinaturas

### Exportando a Chave
```gpg --armor --export 38A5A08F2FE7B666```

Este comando vale apenas para a sessão, se quiser manter por default, edite o arquivo bash_profile inserindo esta linha nele e salvando.

### Salvar as configurações de assinatura no Git
```git config --global user.signingKey "ID_da_chave_gpg"```

Isso fará com que a chave fique configurada de forma global (Para todos os commits) e não apenas para o projeto em questão.

### GPG_TTY
Também é necessário inserir a variável de TTY do GPG no bash_profile.
```vim ~./bash_profile```
```export GPG_TTY=$(tty)```

### Configurando o GIT para assinar os commits e as tags
```git config --global commit.gpgsing true```
```git config --global tag.gpgsign true```
