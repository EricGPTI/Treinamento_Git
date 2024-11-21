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

### Adicionando novo email a sua GPG

Primeiramente é necessário pegar o id da GPG: ```gpg --list-secret-key --keyid-form LONG```

Depois precisamos editar nossa gpg key passando o id da GPG:```gpg --edit-key 38A5A08F2FE7B666```

Isso fará com que um terminal do GPG seje aberto.

No terminal digite ```adduid``` insira todas as informações necessárias, igual a primeira criação e finalize digitando *O*

Você perceberá que uma nova chamve com o nome *unknowns* será criada.

Agora, para tornar essa chave como confiável selecione a chave 2: ```uid 2``` isso selecionará a chave 2. Depois digite ```trust``` e um grupo de opções será apresentado para que você possa dizer o quão confiável é esta nova chave. O número *5* torna a chave *ultimate*. Depois será necessário salvar com o comando ```save``` e pronto, novo email inserido com sucesso!

Digitando novamente ``` gpg --edit-key GPG_Key_Id``` você perceberá que agora ambos os perfis estão como *ultimate*

# Templates para PRs

Para criar um template de Pull Request, basta procurar um modelo que seja do seu agrado, adaptar o modelo ao seu padrão de trabalho e agora precisamos fazer algumas configurações.

### Criando Diretório .github
É necessário criar um diretório chamado *.github*. Dentro deste diretório, vamos criar um arquivo de README chamado *PULL_REQUEST_TEMPLATE.md*

Colar o texto dentro do arquivo de pull_request_template.

Salve e faça o commit do arquivo, depois faça o push do arquivo.

# CODE OWNER
### Justificativa
Quando estamos trabalhando em times, é comum que tenhamo pessoas especializadas em determinadas linguagens ou mesmo em determinados módulos, seja porque o mesmo é o arquiteto, ou porque é o mais velho, ou ainda porque foi o criador, não importa, o ponto é que sempre teremos alguém que conhece muito de uma determinada parte do código ou expert em uma linguagem. 

A questão é, quando precisamos fazer um code review, faz sentido entregar um code review de um código python a um dev C#? Ou ainda, faz sentido entregar um code review de um módulo do backend a um dev frontend?

A ideia de se trabalhar com codeowner é justamente fixamos a responsabilidade de revisão a pessoas que façam sentido.

### Preparando
Dentro do diretório *.github* devemos criar um arquivo chamado *CODEOWNERS*

Dentro deste arquivo, configuramos quais arquivos serão revisados por quem... Veja um exemplo.

```
*.py @EricGPTI
```
O que acabamos de fazer foi dizer que, todo arquivo .py deverá ter como reviewer o colaborador que tem o perfil chamado @EricGPTI.

A partir de agora, toda vez que fizermos um *Pull Request*, será obrigatório a revisão por este colaborador. 

O mesmo vale para diretórios.
