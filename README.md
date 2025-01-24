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

<h1>CAP 1- CURSORES</h1>

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

Instrução FETCH para recuperar os daods do conjunto ativo, uma de cada vez. A cada extração, o Cursor avança para a próxima linha no conjunto ativo.
 
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
