 ## Comandos Úteis Git 
 
# Iniciando um Repositório 
 
Todo repositørio Git armazena as informações dentro de uma pasta oculta chamada “/.git”. Para que os arquivos de uma pasta possam ser versionados pelo Git, é preciso iniciar o repositório. Basta executar o comando abaixo:
 
> $ git init

# Apagando um repositório

Há momentos em que não queremos apagar nossos arquivos, mas queremos remover as informações sobre aquele repositório criado com o $ git init (talvez criar um repositório novo com os mesmos arquivos). Para isso não usamos o Git. Lembre-se que um repositório Git armazena as informações dentro de uma pasta oculta chamada /.git. Então basta apagar esta pasta oculta que o seu atual diretório deixará de ser um repositório.

> $ rm -rf .git

# Listando arquivos modificados

Esse comando indica o estado do seu repositório. Em outras palavras, ele vai listar todos os arquivos que foram modificados desde o seu último commit.

> $ git status

# Arquivos não monitorados

Se o arquivo foi modificado mas você ainda não executou git add, um simples git checkout removerá as alterações, deixando o arquivo como ele estava no último commit. Passe o nome do arquivo a ter as alterações desfeitas ou . para desfazer as alterações em todos os arquivos modificados. Muito útil se você está apenas experimentando um código mas não quer que ele seja salvo.

> git checkout .

Esse comando não apaga novos arquivos. Para apagar novos arquivos que ainda não foram adicionados ao Stage, execute:

> git clean -df

# Removendo arquivos do Stage

Se você executou git add e quer desfazer, use o reset

> git reset

Para desfazer as modificações, após o reset use o checkout ou clean mostrados anteriormente.

# Desfazendo o último commit

Caso você tenha feito alterações e já tenha chegado a realizar um commit, para desfazer é necessário usar o revert

> git revert HEAD

# Renomear Commit

Escreveu algo errado no último commit? Esse comando te permite renomear a mensagem do último commit feito:

>$ git commit --amend

# Branches

Sempre é bom não trabalhar apenas na main para evitar problemas e ter um projeto mais flexível.

# Listando Branches

Esse comando lista todas as branches presentes no repositório do seu computador.

> $ git branch

Caso você queira que ele liste também as branches que estão no repositório remoto, adicione -a:

> $ git branch -a

# Indo para outra branch

Para mudar para uma outra branch basta usar o comando checkout, passando o nome da branch.

> $ git checkout minha-branch

Se você adicionar -b, uma nova branch será criada.

> $ git checkout -b minha-nova-branch

# Excluindo branches

Para excluir uma branch local basta executar o comando branch com -d ou -D, passando o nome da branch que você quer apagar.

> git branch -d nome-da-branch
git branch -D nome-da-branch

A opção -d é mais segura, pois ela só apaga a branch se você já tiver feito merge ou enviado as alterações para seu repositório remoto, evitando perda de código.

A opção -D ignora o estado da sua branch, forçando a sua remoção.

Esse comando apaga apenas a branch local, não removendo branches remotas.

# Renomeando branches

Para renomear a sua atual branch local, execute o comando branch com a opção -m, passando o novo nome.

> git branch -m novo-nome-da-branch 

Se você estiver em uma branch e quiser renomear outra, você deve passar primeiro o nome atual da branch que quer renomear:

> git branch -m nome-atual novo-nome

# Branch Órfã

Uma branch órfã tem esse nome porque ela não está ligada à branch principal, então seus históricos não são compartilhados.

Isso pode ser útil quando você quer colocar mais de um projeto em um mesmo repositório. Um bom exemplo é quando você tem um projeto no Github e quer criar um site para divulgar o seu projeto. A aplicação e o site são coisas diferentes, portanto os códigos deles devem ser versionados separadamente. Ter ambos em um mesmo repositório simplifica o gerenciamento.

Para criar uma branch órfã basta usar o comando:

> git checkout --orphan minha-branch-orfa

# Visualizando o Histórico de Commits

Para visualizar o histórico de commits basta usar o seguinte comando:

> $ git log

Você ainda pode adicionar mais parâmetros a esse comando, como:

# Histórico de um ou mais arquivos

Mostra o histórico de commits feitos por uma única pessoa

> $ git log --autor=nome-autor

# Histórico por Data

Mostra o histórico de commits feitos antes ou após uma data:

> $ git log --after="MMM DD YYYY"
$ git log --before="MMM DD YYYY"

Exemplo do formato usado nas datas: “Jul 07 2019”

# Histórico Baseado em uma Mensagem

Mostra o histórico de commits filtrado por uma mensagem

> $ git log --grep produtos

Com esse comando teremos o histórico de commits em que a mensagem do commit possua a palavra “produtos”. O que passamos pode ser uma expressão regular, e podemos passar mais de uma:

> // procurar por "produtos" OU "usuarios"
$ git log --grep produtos --grep usuarios

> // procurar por "produtos" E "usuarios"
$ git log --grep produtos --and --grep usuarios

# Exibir branches em um modo mais legível

É possível mandar imprimir o histórico exibindo as branches do repositório com algo mais legível e com cores com um comando. Teremos um resultado parecido com esse:

 * a102055 (HEAD -> main) commit 8
| * 196d28e (branch-2) commit 7
| * 07e073c commit 3
| * 2b077ca new fie
| | * c1369d8 (branch-3) commit 6
| | * d11bdcd commit 5
| |/
|/|
* | 2b22b75 commit 2
|/
* d5a12b0 .gitignore
* 9535426 -- commit 1

O comando é um pouco comprido:

> git log --all --decorate --oneline --graph

Para decorar tudo o que devemos escrever depois de log, lembre-se de A DOG

> –all
–decorate
–oneline
–graph

# Atalhos Personalizados

Podemos criar atalhos para não ficar escrevendo comandos grandes como o do exempo anterior.

# Criando atalhos personalizados

Para criar atalhos personalizados, basta adicionar uma configuração, passando o nome que você quiser para o alias.

Por exemplo, se eu quiser que o comando ensinado anteriormente fosse chamado a partir do atalho dog

> //deixar o comando disponível apenas no repositório atual
git config alias.dog "log --all --decorate --oneline --graph"
//deixar o comando global em sua máquina, ficando disponível para qualquer repositório
git config --global alias.dog "log --all --decorate --oneline --graph"

Como os comandos serão do Git, não precisamos ficar chamando-o. Note que o comando passado para o atalho não inicia com git.

Para remover os atalhos basta executar:,

> //atalhos locais
git config --unset alias.dog
//atalhos globais
git config --global --unset alias.dog

Agora podemos ter o comando do exemplo anterior apenas executando $ git dog.

# Listando atalhos personalizados

Para exibir uma lista de atalhos personalizados, podemos executar o comando git config -l, que lista todas as configurações do seu Git. O problema é que esse simples comando vai listar todas as configurações. Podemos fazer um comando mais sofisticado para ele listar apenas os nossos atalhos personalizados e ainda organizá-los em ordem alfabética:

> git config -l | grep ^alias\. | cut -c 7- | sort

O comando é grande, mas tudo bem, pois agora você sabe criar atalhos, não é mesmo? Podemos, por exemplo, criar um atalho com o nome alias:

> git config alias.alias "! git config -l | grep ^alias\. | cut -c 7- | sort"

Por comandos como grep e sort não serem do Git, tivemos que iniciar a linha de comando com !. Perceba que por causa disso, nossa primeira instrução teve que chamar o Git.

O $ git config -l lista as configurações do Git. Pegamos o retorno e passamos ao comando $ grep, que serve para fazer busca de textos. Como queremos os atalhos, que vimos que começa com “alias”, mandamos o grep buscar por tudo que começa com alias.. Para termos uma lista mais limpa, usamos o comando cut para remover a parte “alias.” do nome dos atalhos. Por fim, usamos o comando sort para ordenar nossos atalhos em ordem alfabética.

# Trabalhando em mais de uma coisa sem fazer commit

Pode haver momentos em que você precisa parar o que está fazendo e começar a trabalhar em outra tarefa. Porém, pode não ser bom fazer o commit de algo que ainda não foi finalizado para depois voltar nele, resultando em um commit que ficará no histórico mas que possui um código que não funciona. Nós podemos salvar essas alterações feitas mesmo sem precisar realizar um commit para depois voltar a trabalhar nela, o que é chamado de Stash (algo como “esconder” ou “acumular”).

Ao fazer isso, seu repositório voltará ao estado do último commit, e as alterações feitas anteriormente estarão “escondidas”.

# Salvando modificações em um Stash

Simplesmente execute o comando stash

> $ git stash

Você ainda pode colocar um nome nesse stash:

> $ git stash push -m meu-novo-stash

# Listando Stashes

Você pode fazer vários stashes. Para listá-los, execute o comando:

> $ git stash list 

# Recuperando modificações

Se algo foi salvo no stash, basta executar o seguinte comando para recuperar as alterações que foram jogadas lá:

> $ git stash apply

Isso vai recuperar o código do stash mais recente. Se quiser recuperar um stash mais antigo, basta ver o número do stash que aparece quando o listamos e passar para o seguinte comando: 

> $ git stash apply stash@{2}

# Removendo Stashes

Quando nós recuperamos alterações de um stash, ele continua guardado. Para apagá-lo da pilha, execute o comando drop junto ao nome do stash que você quer remover:

> $ git stash drop stash@{5}

Se você quiser recuperar o código de um stash e já apagá-lo, pode usar o comando pop no lugar do apply.

# Juntando alguns pedaços do trabalho

Pode ser que você esteja trabalhando em uma branch e queira fazer o merge do código dela com outra branch, mas não quer juntar o trabalho inteiro, apenas um commit específico. Isso é possível com o Cherry Pick.

> git cherry-pick id-do-commit


* Considerações finais: relatório baseado no conhecimento desenvolvido na DIO e também baseados em informações na Web. 









