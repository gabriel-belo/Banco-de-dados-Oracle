# Banco-de-dados-Oracle
Aprendendo  sobre Banco de dados Oracle  com curso da FIAP "Banco de Dados Oracle"

<h1>CAP 1- Apresentação da disciplina</h1>

<h3>Histórico</h3>
O significado do nome PL/SQL é "Procedual Language extensions to SQL". É muito similar ao SQL, mas incorpora funcionalidade de outraslinguagens de programação, tornando-a uma linguagem poderosa para a manipulação de dados.

No SQL Server é usado o Transact-SQL, no MySQL temos uma linguagem para procedimentos também, no PostgreSQL temos uma linguagem chamada PGPLSQL

<h1>Preparando o ambiente</h1>
Utilize o seguinte para saber a quantidade de linhas na tabela  SELECT COUNT(*) From nome_tabela; 

Para apagar uma tabela utilize DROP TABLE nome_tabela PURGE

NUMBER(2,0) significa número inteiro com até dois dígitos 
VARCHAR2(14) Alfanumérico com até 14 caracteres

Um bloco é a unidade básica de programação do PL/SQL. Em um bloco PL/SQL podem-se usar comandos SQL, como o SELECT, INSERT, UPDATE e DELETE, e usar instruções como IF - THEN - ELSE.

Existem dois tipos de blocos os anônimos e os nomeados 

Um bloco anônimo é um conjunto de instruções que não fica armazenado definitivamente no banco. O conjunto de instruções é interpretado, executado e, mais tarde, descartado.

O bloco nomeado é um conjunto de dados de instruções que fica armazemnado no banco de dados.

Podemos dividir o bloco PL/SQL em quatro seções:

Declarativa(opcional)- Seção destinada à declaração das variáveis, cursores e exceções que serão utilizadas no bloco. É iniciado pela palavra DECLARE e, caso seja definida, deve ser a primeira estrutura do programa.

Executável(obrigatório)- também conhecida como corpo de programa, área em que são escritos os passos necessários para realização. Podem ser usadas instruções SQL ou PL/SQL. É iniciado pela palavra BEGIN

Tratamento de exeções(opcional)- destinada ao tratamento das exeções geradas no bloco; deve, ser descritas as ações a serem desempenhadas quando ocorrem erros. É iniciado pela palavra EXCEPTION

FIM(obrigatório)- destinadp ao encerramento do programa. Todo programa PL/SQL deve ser finalizado usando a palavra END

É comum terminar o bloco com / quando estamos trabalhando com a interface SQL*Plus, este caractere  encerra o editor PL/SQL e executa o bloco.

<h3>Variaveis</h3>

Tipos de variáveis:
<ul>
  <li>Variáveis escalaveis: São as que armazenam apenas um tipo de valor</li>
  <li>Variáveis compostas: Nelas é possível guardar mais de um tipo de valor por vez. Os tipos compostos em PL/SQL são registros, tabelas e matrizes</li>
  <li>Variaveis referênciais: Armazenam valores, chamados de indicadores, que designam outros itens de programa. Um exemplo de tipos referênciais é o REF CURSOR</li>
  <li>Variáveis BLOB ou CLOB  ou LOB(LARGE OBJECT): utilizados para guardar binários, usados para guardar arquivos, imagens gráficas, videoclipes entre outros, de até 4 gigabytes em tamanho</li>
</ul>

As variaveis LOB podem ser classificadas como: 
<ul>
  <li>CLOB(character large object): É usado para armazenar blocos grandes de dados com caracteres de um único byte no banco de dados</li>
  <li>BLOB(binary large object):É usado para armazenar objetos binários grandes no banco de dados em linha (dentro de uma linha da tabela) ou fora da linha (fora da linha de tabela)</li>
  <li>BFILE(binary file): É usado para armazenar objetos grandes binários em arquivos do sistesma operacional fora do banco de dados</li>
  <li>NCLOB: É usado para armazenar blocos grandes de dados NCHAR de byte único ou de bytes múltiplos de largura fixa de dados, dentro e fora de linha</li>
</ul>

<h3>Tipos de dados escalares</h3>
Um tipo de dados escalares armazena um valor único e nção possui componentes internos. Os tipos de dados escalares podem ser classificados em quatro categorias: número, caractere, data e booleano.

Tipos de dado:
<ul>
  <li>VARCHAR32: Armazena caracteres com tamanho variável com até 32.767 bytes; Não a tamanhao padrão para estas variáveis</li>
  <li>Number: Armazena números reais ou inteiros</li>
  <li>DATE: Armazena datas e horas</li>
  <li>CHAR:Armazena caracteres com tamanho fixo até 32.767 bytes;tamanhao padrão de 1 byte</li>
  <li>BOOLEAN: Armazena um de três valores possíveis: TRUE, FALSE ou NULL</li>
  <li>BINARY_INTEGER: Armazena números inteiros entre -2.147...  e 2.147...</li>
  <li>PLS_INTEGER: Armazena números inteiros entre -2.147...  e 2.147...; estes valores requerem menos armazenamento e são mais rápidos que os valores NUMBER e BINARY_INTEGER</li>
</ul>

As declarações poderão também atribuir um valor inicial e impor a restrição NOT NULL

Na nomeação das variáveis é usado o underline para separar palavras
Padrão de nomeação: v_nome_variavel

Para nomeação de constantes usamo: c_const

É possível carregar uma atribuição para uma variavel utilizando ":="
Outra forma:
Select nome_coluna
into v_variavel
from nome_tabela

Para jogar informações na tela devemos usar a biblioteca DBMS_OUTPUT e o comando .PUT_LINE();
Para que a biblioteca funcione é necessário usar este comando antes dela SET SERVEROUTPUT ON

<h3>Instrução SELECT em PL/SQL</h3>
Utilizar a intrução SELECT para recuperar dados do banco de dados. A instrução precisa usar uma estrutura denominada CURSOR para recuperar mais de uma linha de uma vez. Para recuperar apenas uma linha usamos a esturuta: 
SELECT  colunas
INTO	 {variáveis...| registro}  
FROM	 tabela
WHERE	 condição;

Para adicionar variaveis ao output:
DBMS_OUTPUT.PUT_LINE(‘A soma dos salários do departamento ‘ || v_deptno || ‘ é ‘ || v_soma_sal);

Para somar elementos usamos o método SUM()

<h3>Instrução INSERT</h3>
Podemos usar a intrução INSERT para incluir dados em uma tabela.
A esturuta para esta intrução consiste em dizer em qual tabela será adiciona e as colunas
e depois passar os valores a serem adicionados
   INSERT INTO emp(empno, ename, job, deptno)
          VALUES (v_empno, v_ename, v_job, v_deptno);

<h3>Instrução UPDATE</h3>
A intrução UPDATE é utilizada para atualizar dados em uma tabela 
Exemplo:
DECLARE
	v_sal_increase   NUMBER := 2000;
BEGIN
	UPDATE	emp
	SET		sal = sal + v_sal_increase
	WHERE	job = 'ANALYST';
END;
/

<h3>Instrução DELETE</h3>
A instrução DELETE é utilizada para deleatr elementos de uma tabela
Exemplo:
DECLARE
	v_deptno   NUMBER := 10;               
BEGIN							
	DELETE FROM   emp
	WHERE         deptno = v_deptno;
END;
/

<h3>Controle de transação</h3>
Uma trnasação consiste em uma ou mais intruções SQL, as quais, quando executas, podem ser consideradas como uma única  unidade. O que significa que se uma instrução de transição falhar, a transação inteira falha 
Ele funciona para situações em que necessitamos que ou funcione todas as transações ou nenhuma


<h1>CAP 2- ESTRUTURA DE CONTROLE</h1>
<h3>Tipos de dados</h3>

Para fazer modificação no tipo de dado de uma coluna usamos
ALTER TABLE tabela1
MODIFY com1 VARCHAR2(30);

Porém caso a tabela tenha uma cokuna maior do que o tamanho definido para a variável no bloco PL/SQL ocorrera um erro

Uma forma de evitar este problema é declararmos a variável com o atributo %TYPE
Utilizando o %TYPE dizemos que queremos que uma variavel tenha um tipo de dado similar ao presente em outro lugar
Exemplo:
v_col1 tabela1.col1%TYPE

<h3>Estruturas de seleção</h3>
As estruturas de controle permitem que o desenvolvedor estabeleça o fluxo lógico de instruções que serão executadas.

As estruturas de seleção possibilitam que o fluxo de processamento das instruções PL/SQL seja direcionado de acordo com a condição especificada.

Três maneiras de utilizar a instrução IF:
<ul>
	<li>IF THEN</li>
	<li>IF THEN ELSE</li>
	<li>IF THEN ELSIF</li>
</ul>

Como usar o IF THEN:
IF (condição) THEN
	conjunto de instruções;
END IF;

A condição pode receber como resultado TRUE, FALSE e NULL porém só será executada se receber TRUE como resposta
As instruções podem receber comandos SQL ou PL/SQL. Podem incluir mais instruções IF contendo diversos IFs, ELSEs e ELSIF aninhados

Pode usar qualquer quantidade de ELSIF, mas só pode haver, no máximo uma cláusula ELSE

<h3>Utilizando IF THEN ELSE</h3>
IF (condição) THEN
	conjunto de instruções 1;
ELSE
 	conjunto de instruções 2;
END IF;

<h3>IF THEN ELSIF</h3>
IF (condição1) THEN
	conjunto de instruções 1;
ELSIF (condição2)
 	conjunto de instruções 2;
ELSE
	conjunto de intdtruções n;
END IF;


<h3>AND e OR</h3>
Para testar mais de uma condição dentro de uma estrutura de decisão podemos usar os operadores lógicos AND e OR.
Exemplo usando AND
DECLARE 
	v_tamanho NUMBER(3);
 BEGIN
 	SELECT LENGTH(col1) INT v_tamanho
  	FROM tabela1
   IF v_tamanho > 25 AND TO_CHAR(SYSDATE, 'YYYY') > 1999 THEN
   	DBMS_OUTPUT.PUT_LINE('Maioe que 25 bytes e século XXI')
    END IF;
END;
/

Exemplo usando OR:
DECLARE 
	v_tamanho NUMBER(3);
 BEGIN
 	SELECT LENGTH(col1) INT v_tamanho
  	FROM tabela1
   IF v_tamanho > 25 ORTO_CHAR(SYSDATE, 'YYYY') > 1999 THEN
   	DBMS_OUTPUT.PUT_LINE('Maioe que 25 bytes e século XXI')
    END IF;
END;
/

Também temos o operador NOT que modifica o TRUE para FALSE e vise versa, porém o NULL continua NULL.

<h3>ESTRUTURA DE REPETIÇÂO</h3>
Utilizados para que algo seja executado repetidas vezes.
Nem todas as estruturas de repetição possuem resursos para fazer contagem do número de vezes que o laço deverá ser repetido, nessas situações, deve-se utilizar uma variável de apoio sempre do tipo int

Tipos de loop:
<ul>
	<li>Loop básico: para fornecer ações repetitivas sem condições gerais</li>
	<li>Loop FOR: para fornecer controle iterativo para ações com base em uma contagem </li>
	<li>Loop WHILE: Para fornecer controle iterativo para ações com base em uma condição</li>
</ul>

<h3>Loop básico</h3>
Exemplo:
LOOP
	conjunto de instruções;
 	EXIT [WHEN condição]
END LOOP;

<h3>LOOP FOR</h3>
O LOOP FOR realiza as iterações de acordo com a instrução de controle que precede a palavra-chave LOOP.
FOR contador in [REVERSE] num_inicial..num_final LOOP
	conjunto de instruções;
 	. . .
END LOOP;

O REVERSE serve para fazer o contador decrescer a cada iteração a partir do limite superior até o limite inferior. É importante notar que o limite inferior ainda é referenciado primeiro.

Exemplo:
BEGIN
	FOR i IN 1..10 LOOP
 		INSERT INTO tabela1
   		VALUES('Inserindo texto numero' || i)
     END LOOP;
END;
/

Os limites superior e inferior da faixa do LOOP podem ser literais, variáveis ou expressões, mas devem ser avalisados para inteiros.

<h3>LOOP WHILE</h3>
Pode ser usado para repetir uma senquencia de instruções até que a condição para controle não seja verdadeira.

WHILE condição LOOP
	 conjunto de instruções 
  	. . .
END LOOP;

Se a condição produzir NULL, o LOOP será ignorado e o controle passará para a próxima instrução

Exemplo: 
DECLARE
  v_contador NUMBER(2) :=1; 
BEGIN   
  WHILE v_contador <= 10 LOOP
    INSERT INTO tabela1
    VALUES ('Inserindo texto numero ' || v_contador);
    v_contador := v_contador + 1;   
  END LOOP;
END;

<h3>LOOP ANINHADO</h3>
É possível aninhar loops básicos, for e while em dentro do outro.
Exemplo:
BEGIN   
  <<loopexterno>>
  FOR i IN 1..3 LOOP
    <<loopinterno>>   
    FOR j IN 1..5 LOOP
        INSERT INTO tabela1
        VALUES ('Inserindo texto numero ' || i || j);
    END LOOP loopexterno;
  END LOOP loopexterno;
END;
/

Para adicionar comentários e ter um código mais intuitivo podemos utilizar um LABEL <<LABEL>>

<h1>CAP 3- CURSORES</h1>

<h3>Tipos de dados</h3>
Para não precisar criar uma variavel para cada coluna e utiliza o %TYPE cada vez que criar uma variavel, podemos usar o atributo %ROWTYPE
O atributo %ROWTYPE fornece um tipo de registro que representa uma linha de uma tabela em um banco de daods relacional. O registro pode armazenar uma linha inteira dos dados, esses podem ser selecionados de uma tabela ou obtidos de um CURSOR ou de uma variavel de CURSOR
*É importante salientar que os campos em um registro definido por %ROWTYPE não herdam as restrições (CONSTRAINTS) e seus valores padrões
A variável não terá as mesmas restrições que a tabela possui e a variável também não herda o valor padrão caso tenha.

Exemplo: 
SET SERVEROUTPUT ON

DECLARE
  emprec emp%ROWTYPE;

BEGIN
SELECT *
  INTO emprec
  FROM emp
 WHERE empno = 7839;
 DBMS_OUTPUT.PUT_LINE ('Codigo   = ' || emprec.empno);
 DBMS_OUTPUT.PUT_LINE ('Nome     = ' || emprec.ename);
 DBMS_OUTPUT.PUT_LINE ('Cargo    = ' || emprec.job);
 DBMS_OUTPUT.PUT_LINE ('Gerente  = ' || emprec.mgr);
 DBMS_OUTPUT.PUT_LINE ('Data     = ' || emprec.hiredate);
 DBMS_OUTPUT.PUT_LINE ('Sala     = ' || emprec.sal);
 DBMS_OUTPUT.PUT_LINE ('Comissao = ' || emprec.comm);
 DBMS_OUTPUT.PUT_LINE ('Depart.  = ' || emprec.deptno);  
END;
/

<h3>Tipos de cursores</h3>
Ao processar uma instrução de SQL, o banco de dados Oracle atribui uma área de trabalho na memória para a execução da instrução SQL. Essa área de memória é denominada área de contexto ou área SQL privada(Private SQL area). Está área armazena informações necessárias para executar a instrução SQL.
Na área de contexto podemos encontrar: O número de linhas processadas, um apontador e, no caso de consultas, o conjunto ativio

O CURSOR é o apontador da àrea de contexto. Um CURSOR permite que nomeie uma instrução SQL, acesse a informação em sua área de contexto e, até certo ponto, controle seu processamento

Existem dois tipos de CURSORES> Cursores Implícitos e Cursores Explícitos

<h3>Cursor Implícito</h3>
Um cursor implícito não é declarado, é criado sem a intervenção do usuário para todas as instruções de defimição dos dados (DDL), manipulação dos dados(DML) e instruções SELECT ... INTO que retornam apenas uma linha.  Se a consulta retornar mais de uma linha dentro do bloco PL/SQL, um erro será gerado, para corrigir esse erro, declare um cursor 
Quando estamos utilizando um cursor implícito e queremos chamar ele utilizamos o termo padrão SQL

<h3>CURSOR EXPLÍCITO</h3>
Um Cursor explícito deve ser declarado explicitamente na área declarativa (DECLARE) do bloco PL/SQL. Ao usarmos um cursor explícitio, podemos processar várias linhas, controlar a área de contexto e os processor que nela ocorrem

O conjunto retornado pelo cursor explícito é denominado de conjunto ativo. O tamanho de um conjunto ativo depende da quantidade das linhas em uma tabela que atendam às condições aplicadas em uma consulta. O cursor explícito identifica a linha que está sendo processada no momento, esta é chamada de linha atual.

EXEMPLO:
DECLARE
	CURSOR cursor_emp IS 
 	SELECT deptno, SUM(sal) #SUM(sal)= soma do salário de todas as pessoas do departamento 
  	FROM emp
   	GROUP BY deptno;
BEGIN
	OPEN cursor_emp;
 END;
 /

Instrução FETCH para recuperar os dados do conjunto ativo, uma de cada vez. A cada extração, o Cursor avança para a próxima linha no conjunto ativo.

Recuperação de linhas do cursor
Através do comando FETCH nós iremos carregar os dados do conjunto, uma linha de cada vez. Após cada extração, o CURSOR avança para apróxima linha no conjunto ativo.

Deve-se incluir o mesmo número de variáveis na claúsula INTO da instrução FETCH do que as colunas na instrução SELECT, as variáveis devem ser do mesmo tipo de dado da coluna correspondente 
A instrução FETCH deve ser executada até que todas as linhas de dados sejam extraídas.

Para fechar o cursor usamos o comando CLOSE nome_cursor;

<h3>LOOPS DE CURSOR FOR</h3>
Base de exemplo:
FOR nome_registro(variavel temporaria que ira carregar este cursor)  IN nome_cursor LOOP
	instruções;
 END LOOP;

Usado um CURSOR FOR o CURSOR é aberto automaticamente, sem necessidade de declará-lo e abri-lo automaticamente.
Durante a repetição do LOOP, os dados são extraídos e processados um a um. Assim que todas as linhas(tuplas) disponíveis forem processadas, o loop termina automaticamentee o cursor é fechado sem que precise executar os comandos em linha 
Não é necessário utilizar o %ROWTYPE pois o loop for já ira criar a variável.

<h3>LOOPS FOR DE CURSOR USANDO SUBCONSULTA</h3>
O CURSOR pode ser substituído por uma subconsulta dentro do loop FOR. Não será possível fazer referência aos atrivutos de CURSOR explícito se usar uma subconsulta em um loop FOR de CURSOR, pois não poderá dar um nome explícito
No exemplo a baixo iremos eliminar a sessão declarativa, tanto registro como o CURSOR são definidos dentro do LOOP FOR
exemplo: 

<h3>CURSORES DE ATUALIZAÇÃO</h3>
Utilizando o FOR UPDATE faz com que as linhas específicas de uma tabela sejam bloqueadas para garantir que nenhuma alteração será efetuada nessas linhas após lê-las e serem alocadas no conjunto ativo
Usamos o comando UPDATE para atualizar
Utilizando o WHERE CURRENT OF podemos fazer a atualização para cada linha de forma específica, sem ocorrer uma atualização instântanea e dar um erro na atualização dos dados. Será atualizada a linha que foi previamente buscada pelo FETCH.
O comando NOWAIT diz ao Oracle que não aguarde, se as linhas solicitadas foram bloqueadas por outro usuário
Exemplo:
DECLARE
  emprec emp%ROWTYPE;   
  CURSOR cursor_emp IS 
         SELECT empno, sal             
          FROM emp
            FOR UPDATE; 
BEGIN
   OPEN cursor_emp;
   LOOP
      FETCH cursor_emp INTO emprec.empno, emprec.sal;
      EXIT WHEN cursor_emp%NOTFOUND;
      UPDATE emp SET sal = sal * 1.05 WHERE CURRENT OF cursor_emp;
   END LOOP;
   CLOSE cursor_emp;
END;
/

 
<h1>COMANDO APRENDIDOS</h1>
<ul>
	<li>SUM() faz a soma </li>
	<li>LENGTH() calcula o comprimento</li>
	<li>ROLLBACK desfaz a ação, é como um retornar no word</li>
</ul>

<h1>COMANDO PARA USAR NOS CURSORES</h1>
<ul>
	<li>%FOUND retorna verdadeiro caso alguma linha(tupla) tenha side afetada</li>
	<li>%ISOPEN retorna verdadeiro caso o CURSOR esteja aberto</li>
	<li>%NOTFOUND retorna verdadeiro caso não tenha encontrado nenhuma tupla(linha)</li>
	<li>%ROWCOUNT retorna o número de tuplas(linhas) do CURSOR</li>
</ul>

<h1>Comando dos cursores implícitos</h1>
<ul>
	<li>%BULK_ROWCOUNT</li>
	<li>%BULK_EXCEPTION</li>
</ul>


<h1>CAP 4- INTRODUÇÃO AOS OBJETOS COMPILADOS NO ORACLE RDBMS</h1>
<h3>Dicionário de dados</h3>
Um dicionário de dados é um conjunto de Metadados(Dados que descrevem outros dados. Fornecem informações sobre estrutura, formato e conteúdo de um conjunto de dados), que são dados sobre dados. O dicionário de dados fornece uma descrição sobre o banco de dados , temos informações sobre a estrutura física, lógica e seu conteúdo. Consiste numa série de tabelas  e views.

Existem três tipos de views que permitem a consulta do dicionário de dados:
<ul>
	<li>As views USER_ fornecem informações sobre os objetos de propriedade do usuário conectado, Exemplo: Se logar como aluno, ao executar a query(SELECT * FROM USER_OBJECTS) obterá informações sobre os objetos que você criou.</li>
	<li>As views ALL_ fornecem informações sobre os objetos a que o usuário tem acesso. Exemplo: Se quiser ver os objetos a que você tem acesso (incluindo os que pertencem a outros usuários) use a query (SELECT * FROM ALL_TABLES)</li>
	<li>As views DBA_ são de acesso exclusivo dos administradores do banco de dados e fornecem informações de todos os objetos do banco de dados. Exemplo: Um administrador pode executar a seguinte query(SELECT * FROM DBA_TABLES) para ver todas as tabelas do banco de dados.</li>
</ul>

Exemplos: 
1º Serão listados todos os tipos de objetos criados pelo usuário conectadp no momento, usamos o comando DISTINCT para eliminar duplicidade dos objetos nessa listagem.
SELECT DISTINCT object_type
FROM user_objects;

2º Serão listados todos os tipos de objetos a que o usuário conectado no momento de acesso.
SELECT DISTINCT object_type
FROM all_objects;

<h3>Objetos PL/SQL armazenados</h3>
Os objetos PL/SQL armazenados são procedimentos, gatilhos, funções e pacotes. Todos esses objetos são armazenados no dicionário de dados com o seu código-fonte e com a sua compilação. Toda vez que um objeto PL/SQl armazenado é chamado por uma sessão é lido a partir  do dicicionário de dados ou, caso tenha sido executado anteriormente e estiver disponível, a partir da memória CACHE(é uma memória de armazenamentop temporário que armazena informações que são frequentemente acessadas visando acelerar processo de leitura e execução. É um atalho que o sistema usa para acessar dados já utilizados.)

Blocos PL/SQl anônimos são programas PL/SQl não-nomeados e cujo o código não fica armazenado no banco de dados (estes foram os utilizados até agora). A desvantagem de utilizar blocos anônimos é que precisam ser compilados toda vez que vão ser executados e não podem ser chamados por outras aplicações. Se quier reexecutar um bloco PL/SQL anônimo, é necessário executar o SCRIPT com o bloco anônimo novamente. 

Ao usarmos blocos PL/SQL nomeados temos vantagens como: procedimentos e funções são armazenados no banco de dados em formato compilado, e haverá necessidade de recompilar o código caso ocorram modificações no código ou em seus objetos dependentes. Outra vantagem é  que outras aplicações e/ou usuários podem executá-las, desde que possuam os previlégios e autorizações para tal. Além disso, podemos passar parâmetros para os programas e, no caso das funções, podemos obter um retorno.  

Existem view com informações sobre os objetos

<h3>Exibir informações sobre os objetos armazenados</h3>
Cada linha da view user_object contém informações dos seus objetos do banco de dados
Exemplo:
SELECT object_name
FROM user_objects
WHERE object_type= "TABLE"
ORDER BY object_name
/
No exemplo recebemos uma listagem com o nome de todos os objetos do tipo TABLE pertencentes ao usuário que está executando a consulta. Para obter uma listagem com o nome de todos os objetos do tipo TABLE que o usuário que está executando a consulta possui acesso, basta substituir o nome da view USER_OBJECTS por ALL_OBJECTS
O ORDER BY é usado para ordenar os resultados em uma consulta, define a sequência em que os registros serão exibidos na saída. A ordem padrão é do menor para o maior, isso significa que os resultados serão organizados primeiro por object_type no caso do exemplo.
O WHERE é como um filtro. 

O STATUS de um programa PL/SQL armazenado é definido como INVALID quando o objeto do qual é dependente é alterado. Os programas com o STATUS de INVALID devem ser recompilados. A recompilação pode ser feita manualmente ou automaticamente. A automática será feita na próxima vez que o banco de dados tentar executar o programa 


<h3>Exibir informações sobre o código-fonte</h3> 
O código-fonte de todos os programas PL/SQL que foram compilados com sucesso estão disponíveis por meio do view USER_SOURCE. 
Podemos obter várias informações significativas, por exemplo:
<ul>
	<li>Descobrir quais programas usam um determinado valor literal que precisa ser alterado</li>
	<li>Verificar se os padrões de nomes de variáveis da empresa estão sendo obedecidos </li>
	<li>Encontrar todos os programas PL/SQL que chama um determinado procedimento e/ou função e/ou pacote</li>
</ul>

Exemplo:
SELECT name, line, text
FROM user_source
WHERE UPPER(text)
LIKE '%DEPT%'
ORDER BY name, line
/

O exemplo fornece uma listagem com o nome do programa, número da linha e o texto do código-fonte que trabalha com a tabela DEPT. Como é um texto, o exemplo também pode retornar linhas comentadas que possuam a palavra DEPT ou variáveis que possuam a palavra  DEPT em seu nome.

<h3>Exibir informações sobre procedimentos e funções</h3>
As informações sobre os procedimentos efunções criadaqs pelo usuário podem ser obtidas por meio da view USER_PROCEDURES
Exemplo:
SELECT object_name, procedure_name
FROM user-procedures
WHERE authid= 'CURRENT_USER'
ORDER BY object_name, procedure_name
/
Fornece uma listagem com o nome do objeto e o nome das funções e procedimentos que serão executados usando os privilégios de execução do usuário que executa o programa

<h3>Exibir informações sobre gatilhos (TRIGGERS)</h3>
As informações sobre os gatilhos(TRIGGERS)(gatilhos são como alarmes programados dentro de um banco de dados. Eles são usados para executar automaticamente ações específicas em resposta a certos eventos que ocorrem em uma tabela) podem ser obtidas por meio da view USER_TRIGGERS

SELECT * FROM user_triggers
WHERE status= 'DISABLED'
/
Fornece uma listagem com informação sobre todos os gatilhos desabilitados criado pelo usuário conectado ao banco de dados.

SELECT * 
FROM user_triggers
WHERE table_name= 'EMP'
AND trigger_type LIKE '%EACH ROW'
/
Fornece uma listagem com informações sobre todos os gatilhos associados à tabela EMP e que são executados em nível de linha 

<h1>CAP 5- Tratamento de exceções</h1>  
Os erros podem ocorrer durante a compilação ou durante a execução do programa. Os erros de compilação estão associados à sintaxe  das instruções. Neste tipo de erro o compilador da linguagem informa ao programador durante a tentativa de executar uma instrução a ocorrência do erro 
 
Erros em tempo de execução que também são conhecidos como erros de RUNTIME, estão associados à utilização do programa. Nesse caso, quando as exceções não são previstas entartadas, o erro gerado interrompe o processamento e uma mensagem de erro é devolvida para a aplicação

Uma exceção é, na verdade, uma ocorrência não esperada ou diferente daquela programada para ser executada, ou seja, uma exceção é um erro

A estrutura da seção de tratamento de exceções:
EXCEPTION
WHEN exceção1 [OR exceção2 ...] THEN
	comando1;
 	comando2;
  	...
[WHEN exceção3 [OR exceção4 ...] THEN
	comando1;
 	comando2;
...]

[WHEN OTHERS THEN
	comando1;
 	comando2;

EXCEPTION indica o início da seção de tratamento
WHEN filtra quais exceções devem receber quais comandos 
Podemos utilizar o OR para adicionar mais de uma exceção a um filtro 
O OTHERS indica uma cláusula de tratamento de exceções opcional que intercepta qualquer exceção que não foi explicitamente tratada

<h3>Exceções predefinidas nomeadas</h3>

O PUTLINE é utilizado no momento de desenvolvimento do código, utilizamos tabela para armazenar as informações quando estamos na aplicação

O oracle predefiniu exceções para alguns erros mais comuns. Nesses casos, não existe a necessidade de as exceções serem declaradas para serem utilizadas, elas fazem parte do pacote STANDARD.   
Nós utilizamos uma tabela para armazenar os erros nela guardamos por linhas as informações(usurario, data, codigo do erro e msg do erro) para que depois possamos ver os erros e arrumarmos. 
As exceções não podem aparecer em instruções de atribuição ou instruções SQL.

<h3>Funções para a captura de erro</h3>
Quando ocorre uma exceção, pode-se identificar o código ou a mensagem de erro associado usando duas funções SQLCODE e SQLERRM e com base nos valores do código ou mensagem, pode-se decidir qual a ação subsequente a tomar a partir do erro.
SQLERRM é uma função que retorna a memsagem de erro associada a um código de erro numérico, enquanto SQLCODE tetorna o código numérico de uma exceção
Usamos a função SUBSTR para truncar o tamanho da mensagem de erro para um tamanho conhecido, que é definido na função
Exemplo:
SUBSTR(SQLERRM, 1, 100)

Valores que podem ser assumidos pelo SQLCODE.
<ul>
	<li>Valor 0: nenhuma exceção encontrada</li>
	<li>Valor 1: Exceção definida pelo usuário</li>
	<li>Valor +100: Exceção NO_DATA_FOUND</li>
	<li>Valor número negativo: Número de erro do servidor Oracle</li> 
</ul>

<h3>Exceções nomeadas pelo desenvolvedor</h3>
Uma boa prática para a criação da sua exceção é nomea-la inicialmente por 'e_' 

<h1>CÁP 6- Stroed Procedures</h1>
Vantagens dos blcos PL/SQL nomeados: procedimentos e funções são armazenados no banco de dados em formato compilado. Caso ocorra mudança nos seus objetos dependentes, haverá necessidade de recompilar o código. Outro benefício é a possibilidade de que outras aplicações e/ou usuários podem executá-los, desde que possuam os privilégios e as autorizações. Além disso podemos passar parâmetros para os programas e, no caso, de funções devolver resultados.

O nome do objeto identifica um procedimento. O nome do procedimento, pacote, função ou corpo do pacote pode ser definido por meio dos comandos CREATE PROCEDURE, CREATE FUNCTION, CREATE PACKAGE ou  CREATE PACKAGE BODY.

O compilador PL/SQL analisa o código-fonte que difitou e produz  uma representação da análise do código-fonte. Essa analise é chamada de PARSE TREE ou árvore de analise

O pseudocódigo ou P-CODE é gerado pelo compilador PL/SQL baseado no código analisado ou PARSED CODE. O PL/SQL executa o P-CODE quando solicitamos a execução do procedimento, função ou pacote.

Tanto a P-CODE quanto a PARSE TREE de um procedimento, função ou pacote são armazenados no banco de dados para evitar que sejam recompilados desnecessariamente. O P-CODE é uma representação do que foi analisado e é otimizado para ser executada de forma eficiente.

O fato do P-CODE estar armazenado no banco de dados permite que seja copiado para a memória CACHE do servidor em uma área denominada de SHARED POOL. A SHARED POOL faz parte de uma área de memória denominada SGA ou SYSTEM GLOBAL AREA.

A versão compilada do código permanece em memória baseada em um algoritmo de LRU, ou LEAST RECENTLY USED, em tradução direta, MENOS RECENTEMENTE USADO. Esse alforitmo garante que os códigos que não estão sendo usados serão descartados da memória.

Os códigos-fonte P-CODE e PARSE TREE são armazenados no dicionário de dados do banco de dados. O dicionário de dados fica armazenado no TABLESPACE SYSTEM do banco de dados. Um TABLESPACE é um nime lógico para um ou mais arquivos físicos do banco de dados.

<h3>O PROCEDIMENTO</h3>
Um PROCEDURE envolve basicamente os passos de identificação do procedimento, definição dos parâmetros ou parâmetro, definição do conjunto de instruções do procedimento e submissão do código ao SGBDR.
<h4>O que é o SGBDR</h4>
Significa Sistema de Gerenciamento de Banco de Dados. É um software que permite criar, gerenciar e interagir com bancos de dados que seguem o modelo relacional, que organiza os dados em tabelas interligadas
Características de um SGBDR:
<ul>
	<li>Estrututura de tabela: Os dados são armazenados em tabelas, que consistem </li>
	<li></li>
	<li></li>
	<li></li>
	<li></li>
</ul>
