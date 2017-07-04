# Trabalhando com GIT

## Instalando o GIT no Linux[UBUNTU]

```
sudo apt-get install openssl git-core
```
Siga as instruções do prompt de comando, primeiro confirmando a instalação dos pacotes e suas dependências, depois confirmando a instalação do pacote git-core

##Criando uma chave SSH para utilizar no [GITHUB](https://github.com)

```
ssh-keygen -t rsa -C "seu_email@provedor.com"
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



## Configuração do repositório do remoto GIT

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
