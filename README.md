# Linux Comandos
O "Terminal" é puramente baseado em texto e é intimidador no começo. No entanto, se decompormos alguns dos comandos, depois de algum tempo, você rapidamente se familiarizará com o uso do terminal!

É assim que se parece um terminal
tryhackme@linux1:~$ enter commands here
Precisamos ser capazes de fazer funções básicas como navegar para arquivos, exibir seus conteúdos e criar arquivos! Os comandos para fazer isso são autoexplicativos (quando você sabe o que são, é claro...)


Vamos começar com dois dos primeiros comandos que eu dividi na tabela abaixo:

Comando	Descrição
echo	Produza qualquer texto que fornecermos
whoami	Descubra com qual usuário estamos conectados no momento!

Usando echo
tryhackme@linux1:~$ echo "Hello Friend!"

Usando whoami para descobrir o nome de usuário com quem estamos logados
tryhackme@linux1:~$ whoami

Interagindo com o sistema de arquivos

Como eu disse anteriormente, ser capaz de navegar na máquina em que você está logado sem depender de um ambiente de desktop é muito importante. Afinal, qual é o sentido de logar se não podemos ir a lugar nenhum?

Command	Full Name
ls	listing
cd	change directory
cat	concatenate
pwd	print working directory

Listando arquivos em nosso diretório atual (ls)

Antes de podermos fazer qualquer coisa, como descobrir o conteúdo de quaisquer arquivos ou pastas, precisamos saber o que existe em primeiro lugar. Isso pode ser feito usando o comando "ls" (abreviação de listing)

Usando "ls" para listar o conteúdo do diretório atual
tryhackme@linux1:~$ ls
'Important Files' 'My Documents' Notes Pictures

Na captura de tela acima, podemos ver que existem os seguintes diretórios/pastas:

Arquivos importantes
Meus Documentos
Notas
Fotos

Alterando Nosso Diretório Atual (cd)

Agora que sabemos quais pastas existem, precisamos usar o comando " cd " (abreviação de change directory) para mudar para esse diretório. Digamos que se eu quisesse abrir o diretório "Pictures" - eu faria " cd Pictures ". Onde novamente, queremos descobrir o conteúdo desse diretório "Pictures" e para fazer isso, usaríamos " ls " novamente:

Saída do conteúdo de um arquivo (cat)
Embora saber sobre a existência de arquivos seja ótimo, não é tão útil a menos que consigamos visualizar o conteúdo deles.

Iremos discutir algumas das ferramentas disponíveis para nós que nos permitem transferir arquivos de uma máquina para outra em uma sala posterior. Mas, por enquanto, falaremos sobre simplesmente ver o conteúdo de arquivos de texto usando um comando chamado " cat".

"Cat" é uma abreviação de concatenar e é uma maneira fantástica de exibir o conteúdo de arquivos (não apenas arquivos de texto!).

Na captura de tela abaixo, você pode ver como combinei o uso de "ls" para listar os arquivos dentro de um diretório chamado "Documentos":

Embora não pareça até agora, um dos recursos redentores do Linux é realmente o quão eficiente você pode ser com ele. Dito isso, você só pode ser tão eficiente quanto estiver familiarizado com ele, é claro. Conforme você interage com sistemas operacionais como o Ubuntu ao longo do tempo, comandos essenciais como aqueles que já cobrimos começarão a se tornar memória muscular.

Uma maneira fantástica de mostrar o quão eficiente você pode ser com sistemas como este é usar um conjunto de comandos para pesquisar rapidamente por arquivos em todo o sistema ao qual nosso usuário tem acesso. Não há necessidade de usar consistentemente  cd e  ls para descobrir o que está onde. Em vez disso, podemos usar comandos como  find para automatizar coisas como esta para nós!

É aqui que o Linux começa a ficar um pouco mais intimidador de se abordar — mas vamos explicar isso em detalhes e facilitar para você.

Usando Find
O comando find é fantástico no sentido de que pode ser usado tanto de forma muito simples quanto bastante complexa, dependendo do que você quer fazer exatamente. No entanto, vamos nos ater aos fundamentos primeiro.

Veja o trecho abaixo; podemos ver uma lista de diretórios disponíveis para nós:

Usando "ls" para listar o conteúdo do diretório atual
tryhackme@linux1:~$ ls
Desktop Documents Pictures folder1
tryhackme@linux1:~$

Área de trabalho
Documentos
Fotos
pasta1
Agora, é claro, os diretórios podem conter ainda mais diretórios dentro de si mesmos. Torna-se uma dor de cabeça quando temos que olhar em cada um deles só para tentar procurar por arquivos específicos. Podemos usar findpara fazer exatamente isso para nós!

Vamos começar de forma simples e assumir que já sabemos o nome do arquivo que estamos procurando — mas não conseguimos lembrar onde ele está exatamente! Neste caso, estamos procurando por "passwords.txt"

Se lembrarmos do nome do arquivo, podemos simplesmente usar find -name passwords.txtwhere, o comando procurará em todas as pastas do nosso diretório atual por aquele arquivo específico, assim:

Usando "find" para encontrar um arquivo com o nome "passwords.txt"
tryhackme@linux1:~$ find -name passwords.txt
./folder1/passwords.txt
tryhackme@linux1:~$

"Find" conseguiu encontrar o arquivo — acontece que ele está localizado em folder1/passwords.txt — ótimo. Mas digamos que não sabemos o nome do arquivo, ou queremos procurar por todos os arquivos que têm uma extensão como ".txt". Find nos deixa fazer isso também!

Podemos simplesmente usar o que é conhecido como curinga (*) para procurar por qualquer coisa que tenha .txt no final. No nosso caso, queremos encontrar todos os arquivos .txt que estão no nosso diretório atual. Vamos construir um comando como find -name *.txt. Onde "Find" conseguiu encontrar todos os arquivos .txt e nos deu a localização de cada um:

Usando "find" para encontrar qualquer arquivo com a extensão ".txt"
tryhackme@linux1:~$ find -name *.txt
./folder1/passwords.txt
./Documents/todo.txt
tryhackme@linux1:~$

Find conseguiu encontrar :


"passwords.txt" localizado em "folder1"
"todo.txt" localizado em "Documentos"
Não foi tão difícil, hein!



Usando Grep
Outro ótimo utilitário que é ótimo aprender sobre é o uso de grep. O grepcomando nos permite pesquisar o conteúdo de arquivos para valores específicos que estamos procurando.

Tomemos como exemplo o log de acesso de um servidor web. Neste caso, o access.log de um servidor web tem 244 entradas.

Usando "wc" para contar o número de entradas em "access.log"
tryhackme@linux1:~$ wc -l access.log
244 access.log
tryhackme@linux1:~$
Usar um comando como catnão vai funcionar muito bem aqui. Digamos, por exemplo, se quiséssemos pesquisar este arquivo de log para ver as coisas que um certo usuário/endereço IP visitou? Olhar por 244 entradas não é tão eficiente considerando que queremos encontrar um valor específico.

Podemos usar grep para pesquisar todo o conteúdo deste arquivo para quaisquer entradas do valor que estamos procurando. Seguindo o exemplo do log de acesso de um servidor web, queremos ver tudo o que o endereço IP "81.143.211.90" visitou (note que isso é fictício)

Usando "grep" para encontrar qualquer entrada com o endereço IP "81.143.211.90" em "access.log"
tryhackme@linux1:~$ grep "81.143.211.90" access.log
81.143.211.90 - - [25/Mar/2021:11:17 + 0000] "GET / HTTP/1.1" 200 417 "-" "Mozilla/5.0 (Linux; Android 7.0; Moto G(4))"
tryhackme@linux1:~$
"Grep" pesquisou neste arquivo e nos mostrou todas as entradas do que fornecemos e que estão contidas neste arquivo de log para o IP.

Usando "ls" para listar o conteúdo do diretório atual
tryhackme@linux1:~/Documents$ ls
todo.txt
tryhackme@linux1:~/Documents$ cat todo.txt
Here's something important for me to do later!
Aplicamos alguns conhecimentos adquiridos anteriormente nesta tarefa para fazer o seguinte:

Usado " ls " para nos informar quais arquivos estão disponíveis na pasta "Documentos" desta máquina. Neste caso, é chamado de "todo.txt".
Em seguida, usamos cat todo.txtpara concatenar/exibir o conteúdo deste arquivo "todo.txt", onde o conteúdo é "Aqui está algo importante para eu fazer mais tarde!"

Dica profissional: você pode usar catpara exibir o conteúdo de um arquivo dentro de diretórios sem ter que navegar até ele usando cat  e o nome do diretório. Ou seja,cat /home/ubuntu/Documents/todo.txt

Às vezes, coisas como nomes de usuários, senhas (sim, é verdade...), sinalizadores ou definições de configuração são armazenados em arquivos onde "cat" pode ser usado para recuperá-los.



Descobrindo o caminho completo para nosso diretório de trabalho atual (pwd)
Você notará que, à medida que avança na navegação em sua máquina Linux , o nome do diretório em que você está trabalhando no momento será listado em seu terminal.

É fácil perder a noção de onde estamos exatamente no sistema de arquivos, e é por isso que quero introduzir " pwd ". Isso significa print w orking d irectory.

Usando a máquina de exemplo de antes, estamos atualmente na pasta "Documents" — mas onde isso fica exatamente no sistema de arquivos da máquina Linux? Podemos descobrir isso usando este comando "pwd" como na captura de tela abaixo:

Usando "pwd" para listar o caminho completo do diretório atual
tryhackme@linux1:~/Documents$ pwd
/home/ubuntu/Documents
tryhackme@linux1:~/Documents$
Vamos analisar isso:

Já sabemos que estamos em "Documentos" graças ao nosso terminal, mas neste momento não temos ideia de onde "Documentos" está armazenado para que possamos voltar a ele facilmente no futuro.
Usei o comando " pwd " ( print working directory ) para encontrar o caminho completo do arquivo desta pasta "Documentos" .
O Linux gentilmente nos informou que o diretório "Documentos" está armazenado em "/home/ubuntu/Documentos" na máquina — ótimo saber!
Agora, no futuro, se estivermos em um local diferente, podemos simplesmente cd /home/ubuntu/Documentsmudar nosso diretório de trabalho para o diretório "Documentos".
Símbolo / Operador	Descrição
&	Este operador permite que você execute comandos em segundo plano no seu terminal.
&&	Este operador permite que você combine vários comandos em uma linha do seu terminal.
>	Este operador é um redirecionador, o que significa que podemos pegar a saída de um comando (como usar cat para gerar um arquivo) e direcioná-la para outro lugar.
>>	
Este operador executa a mesma função do >operador, mas acrescenta a saída em vez de substituí-la (o que significa que nada é sobrescrito).

Operador "&"
Este operador nos permite executar comandos em segundo plano. Por exemplo, digamos que queremos copiar um arquivo grande. Isso obviamente levará muito tempo e nos deixará incapazes de fazer qualquer outra coisa até que o arquivo seja copiado com sucesso.

O operador de shell "&" nos permite executar um comando e fazê-lo rodar em segundo plano (como esta cópia de arquivo), permitindo-nos fazer outras coisas!



Operador "&&"
Este operador shell é um pouco enganoso no sentido de quão familiar é para seu parceiro "&". Ao contrário do operador "&", podemos usar "&&" para fazer uma lista de comandos para executar, por exemplo command1 && command2. No entanto, vale a pena notar que command2só será executado se command1for bem-sucedido.



Operador ">"
Este operador é o que é conhecido como um redirecionador de saída. O que isso significa essencialmente é que pegamos a saída de um comando que executamos e enviamos essa saída para outro lugar.

Um ótimo exemplo disso é redirecionar a saída do echocomando que aprendemos na Tarefa 4. Claro, executar algo como echo howdyretornará "howdy" de volta para o nosso terminal — isso não é muito útil. O que podemos fazer em vez disso é redirecionar "howdy" para algo como um novo arquivo!

Digamos que queremos criar um arquivo chamado "welcome" com a mensagem "hey". Podemos executar echo hey > welcomeonde queremos que o arquivo seja criado com o conteúdo "hey" assim:

Usando o operador >
tryhackme@linux1:~$ echo hey > welcome
Usando cat para gerar o arquivo "welcome"
tryhackme@linux1:~$ cat welcome
