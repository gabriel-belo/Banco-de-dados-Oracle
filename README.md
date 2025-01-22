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
