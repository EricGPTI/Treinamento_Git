### Listando GPG Keys existentes
gpg --list-secret-key --keyid-form LONG

Este comando permite que, caso exista uma chave GPG, você pegue o ID da chave para configurações posteriores.

### Gerando GPG Key

```gpg --full-generate-key```

Após isso é só seguir o passo a passo.
Com a chave gerada é hora de utilizar a chave para assinaturas

### Obter a chave GPG para configuração no GIT

```gpg --armor --export 38A5A08F2FE7B666```

De posse da GPG key, vá no git e adicione essa chave.

### Salvar as configurações de assinatura no Git

Para informar ao git qual chave você quer utilizar, use ```gpg --armor``` novamente e pegue o id da chave.
Depois insira o id no git. 

```git config --global user.signingKey "ID_da_chave_gpg"```

Isso fará com que a chave fique configurada de forma global (Para todos os commits) e não apenas para o projeto em questão.

### GPG_TTY

Também é necessário inserir a variável de TTY do GPG no bash_profile como variável de ambiente para não ter que ficar inserindo essa chave o tempo todo..

```
vim ~./bash_profile
export GPG_TTY=$(tty)
```

### Configurando o GIT para assinar os commits e as tags por padrão. Se remover **--global**, a assinatura será apenas para o diretório atual

```git config --global commit.gpgsing true```

```git config --global tag.gpgsign true```

### Guardar senha para que não fique pedindo a senha todas as vezes
```vim ~/.gnupg/gpg.conf```

Aqui você cria um arquivo e dentro dele insere ```use-agent```, salve o arquivo e volte ao terminal.

Depois rode o agente com o comando ```gpgconf --launch gpg-agent```

Pronto, agora não será mais necessário ficar inserindo a senha a todo o tempo. Enquanto o agente estiver rodando, sua senha será salva e não será necessário inser-la a cada commit.

