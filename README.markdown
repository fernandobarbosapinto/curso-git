# Trabalhando com GIT

## Instalando o GIT no Linux[UBUNTU]

```
sudo apt-get install openssl git-core
```
Siga as instruções do prompt de comando, primeiro confirmando a instalação dos pacotes e suas dependências, depois confirmando a instalação do pacote git-core

## Criando uma chave SSH para utilizar no [GITHUB](https://github.com)

```
**ssh-keygen -t rsa -C "seu_email@provedor.com"**
```
Lembre-se de substituir seu_email@provedor.com pelo seu endereço real de email. A resposta do terminal vai perguntar em qual local do seu disco você quer salvar sua chave de segurança. Para evitar problemas, mantenha a opção padrão. A seguir, será solicitada a entrada de uma senha para a chave de segurança. Caso o computador seja público ou compartilhado, é recomendado que sua chave esteja protegida por uma senha. 

Ao término do processo você deve ter dois arquivos com seguintes nomes:

```
id_rsa
id_rsa.pub
```
Ábrir o arquivo id_rsa.pub em um editor de texto simples([TextEditor, Bloco de Notas, GEdit, notepad++, sublime]) e copiar o conteúdo da chave ssh para utilizar nas configurações do github.


## Comandos Básicos do GIT

```
git clone https://github.com/fernandobarbosapinto/curso-git.git
```
Esse comando clone criará uma pasta com o mesmo nome padrão do repositório (que no caso é "curso-git") e copiará para esse diretório todos os arquivos que estavam disponíveis nele.

```
git init
```
Comando utilizado para setar a pasta que será utilizada como nosso repositório.

```
git status
```
Comando utilizado para verificar que o nosso arquivo está na condição de **Untracked files**, isto é, ele não está na lista de arquivos cujas alterações serão rastreadas, ou controladas. Isso acontece porque o Git não sabe que deve controlar as alterações deste arquivo, ou seja, que ele deva fazer o track. Então, como dizemos ao Git que ele deve realizar o track? Isso é feito a partir do comando git add

```
git add nome-do-arquivo.txt
```
Comando utilizado para passar o arquivo a condição de **Changes to be committed**, isto é, na lista de arquivos que estão prontos para o commit

```
git config user.name "Fernando Barbosa Pinto"
git config user.email "fernando.mcsa@gmail.com"
```
Comandos utilizados para configurar o usuário responsável pelas alterações no repositório atual.

```
git config --global user.name "Fernando Barbosa Pinto"
git config --global user.email "fernando.mcsa@gmail.com"
```
Comandos utilizados para configurar o usuário globalmente em todo o sistema.

```
git commit -m "Comentário do commit"
```
Comando utilizado para gravar as alterações do repositório.

```
git tag
```
Comando utilizado para visualizar todas as tags do projeto

```
git checkout v0.1
```
Comando utilizado para entrar na tag v0.1 e visualizar todos os arquivos e como estavam nessa versão. 

```
git diff v0.1 v0.2
```
Comando utilizado para verificar o que foi alterado em cada tag(versão)

```
git blame nome-do-arquivo.txt
```
Comando utilizado para saber o autor da alteração de cada linha do arquivo. Para sair basta apertar **q**.

```
git whatchanged -p
``` 
Ao executarmos o comando [git whatchanged -p] é possível visualizar quais as linhas que foram modificadas em cada commit do nosso projeto. Obs: também é possível utilizarmos [git log -p], que imprime também os commits nos quais não houve modificação.

```
git log
``` 
Comando utilizado para visualização dos commits, é possível também executar o comando git log em um prompt, no diretório de um projeto, que mostrará informações como o autor, a data e hora e a mensagem de commit utilizada.

```
git checkout nome-do-arquivo.txt
``` 
Comando também utilizado para voltar as alterações que foram feitas mas não estão prontas para commit.

```
git reset HEAD nome-do-arquivo.txt (comando utilizado para retirar do estado de INDEX)
git checkout nome-do-arquivo.txt
```
Comando também utilizado para voltar as alterações que foram feitas e já estão prontas para commit (foi feito git add).

```
git log
git reset [copiar a hash do commit que deseja voltar que vai aparecer no git log]
```
Comando utilizado para voltar um commit.

```
git reset --hard HEAD~1
```
Usando esse comando, descartamos definitivamente as mudanças feitas no último commit.

```
git revert [copiar a hash do commit que deseja voltar que vai aparecer no git log]
```
Comando utilizado para voltar um commit qualquer seja ele atual ou antigo.

```
git stash
```
Comando utilizado para guardar alterações temporariamente. Para retornar ao ponto aonde parou basta usar **git stash pop. E se a gente quiser saber se há algum estado salvo via git stash? Isso pode ser feito listando todos os stashes salvos no momento com o comando git stash list. Cada um dos estados salvo é nomeado da seguinte maneira: "WIP on [nome_do_branch]: [hash] [mensagem_do_commit_head]". Também há uma referência ao stash com stash@{0} por exemplo, para o último stash criado. Caso houvessem outros, as referências seriam stash@{1}, stash@{2} e assim por diante.

O comando git stash pop utiliza como padrão o último stash criado. Para aplicar alterações de um stash mais antigo, usamos sua referência:

```
git stash pop stash@{1}
```
```
git stash apply
```
Usando a opção apply, recuperamos as últimas alterações da pilha sem removê-las.

```
git stash drop
```
Este comando faz com que o último estado salvo seja apagado. Também podemos utilizar o nome de cada elemento do stash para remover algum estado que não seja o último. Por fim, se quisermos excluir todos os estados, podemos utilizar o comando git stash clear.

## Configuração do repositório remoto GIT

Para conseguirmos compartilhar nosso projeto HTML, precisamos indicar que o diretório do nosso projeto apontará para um repositório remoto. Para realizarmos esse processo, o Git possui o comando git remote add, com o qual podemos indicar a localização do repositório remoto e o nome que queremos dar para ele (um apelido ou alias).

```
git remote add [alias_do_repositorio] [uri_do_repositorio]
git remote add origin https://github.com/fernandobarbosapinto/curso-git.git
```
Uma convenção adotada é a utilização do nome do repositório remoto como "origin". No entanto, qualquer outro nome pode ser utilizado. Em seguida, devemos saber também a URI do repositório, que é um caminho único que indica o local onde ele ficará armazenado. O próprio Github, segue uma convenção com relação à URI de seus repositórios, sendo a seguinte:

### https://github.com/[nome_do_usuario]/[nome_do_repositorio].git

Com isso, para o nosso projeto, teremos o seguinte caminho:

### https://github.com/[seu_nome_do_usuario]/curso-git.git

## Enviando os commits locais para o repositório remoto

Para isso, uma vez que o repositório já tenha sido inicializado com o comando git init, os commits locais já tenham sido realizados e o repositório remoto configurado, basta executarmos o comando git push, indicando qual é o repositório remoto para onde os commits serão enviados e a branch que será enviada para o servidor. O repositório remoto será o "origin", que acabamos de configurar, enquanto a branch será a "master", criada por padrão sempre que um repositório é criado.

```
git push origin master
```
## Sincronização com as novas alterações do repositório remoto

Para que a sincronização seja realizada e o desenvolvedor tenha em seu computador as novas versões dos arquivos, basta que ele execute o comando:

```
git pull origin master.
```
## Trabalhando com Branch

Sabemos que a utilização de branches facilita no dia a dia do desenvolvedor. Mas como criar uma nova branch? Para tal, utilizamos o comando git branch.

```
git branch ajustes
```
Comando utilizado para criar uma branch.

```
git branch
```
Comando utilizado para visualizar as branchs existentes, lembrando que a branch padrão é a *master.

```
git checkout ajustes
```
Comando utilizado para setar a branch a ser utilizada. Assim todas as alterações relalizadas serão feitas na branch "ajustes".

## Compartilhando uma Branch local com mais desenvolvedores

 Isso é feito utilizando o comando git push passando dois argumentos: o primeiro é o nome do repositório e o segundo, o nome da branch que deseja-se enviar.Porém, toda vez que atualizarmos tanto o nosso projeto local quanto o projeto remoto, precisaremos indicar qual o repositório e o nome da branch que a nossa branch local se refere no remoto, isto é, precisaremos digitar git pull origin design e git push origin design para atualizar os repositórios locais e remotos, respectivamente. Para evitar tal trabalho, podemos indicar o caminho (track) da branch remota para a nossa branch local. Isso pode ser feito no instante em que criamos a branch remota através da opção "-u". No nosso caso, temos:

```
git push -u origin ajustes
```

E como podemos visualizar as branches já existentes em um repositório remoto?

```
git branch -r
```
Esta opção mostra todas as branches, locais e remotas!

```
git branch -a
```
Uma vez visto as branches remotas, como copiar uma delas para a máquina local? Isso é feito passando o nome do repositório e da branch remota ao comando git branch, além de indicar o nome da branch que será criada. Mais uma vez, temos o problema de indicar o caminho entre as branches. Para este caso, a opção -t resolve.

```
git branch -t ajustes origin/ajustes
```

Uma tarefa bem comum é a criação de uma nova branch seguida da troca para essa branch criada. Poderíamos fazer isso com a sequência de comandos **git branch nomeDaBranch** e **git checkout nomeDaBranch**. Mas podemos facilitar isso utilizando a opção -b seguida de qualquer um desses comandos:

```
git checkout -b ajustes 
git branch -b ajustes
```
Uma vez terminada a tarefa pela qual uma branch foi criada, desejamos deletá-la para não poluir muito o nosso projeto com branches que não serão mais utilizadas. Para tal, passa-se um opção ao comando git branch.

```
git branch -d  origin ajustes /remove a branch remota/
git branch -d  ajustes /remove a branch local/
```
*este comando remove uma branch, porém somente se ela estiver sincronizada com outra. Senão, é necessário forçar com a opção -D.*

Num repositório remoto, as alterações são realizadas, geralmente, por mais de uma pessoa ao mesmo tempo. Como saber se foram criadas branches novas no repositório remoto?

```
git fetch origin
```
O comando **git mergetool --tool-help** mostra no console uma lista de programas possíveis de ser utilizados. Dessa lista, pode-se escolher um, instalar no seu computador e utilizar através do comando **git mergetool -t nome_do_programa**.

## Git rebase

Quando estamos no meio do processo de rebase, e houve um conflito que devemos tratar manualmente, como se chama a branch temporária para a qual somos movidos?

** A branch (no branch), que dá a entender que você não está em branch nenhuma, é apenas temporária, criada pelo Git para que possamos resolver o conflito. **

* (no branch)
* desenvolvimento
* master

No processo de rebase, quando há um conflito, temos 3 opções: continue, abort e skip. Podemos continuar um rebase a partir do ponto de conflito, abortar o rebase e voltar ao estado original ou pular o conflito para lidar com ele mais pra frente.



