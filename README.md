# Procedimentos

Procedimentos gerais e referencias sobre scripts/comandos Windows/Linux, gerenciamento de BDs, programação, entre outros

## Gerenciamento do banco de dados

Criar banco: 
Criar usuário: 
Iniciar: 
Parar: 
Backup: 
Restore: 

== INI ==

Alterar senha do usuário administrador do banco de dados

MySQL:
mysqladmin -u root -p<OLDPASSWORD> password <NEWPASSWORD>

== FIM ==

mongodump --host localhost --port 27017 --authenticationDatabase datacare --collection relatorio --db datacare --out D:\Assesso\backup\mongodump201811281059

db.collection.remove({})

mongo --username datacare_dev --password --authenticationDatabase datacare_dev --host localhost --port 27017

Banco de dados PostgreSQL:

Backup PostgreSQL:
"C:\Program Files\PostgreSQL\9.6\bin\pg_dump.exe" --file "D:\\foliveira\\Ferramentas para Dashboard\\Pentaho\\pentaho-dashboards-examples\\pentaho_cde_demo.sql" --host "localhost" --port "5432" --username "postgres" --no-password --verbose --format=p "pentaho_cde_demo"

Restore PostgreSQL:
"C:\Program Files\PostgreSQL\9.6\bin\pg_restore.exe" --host "localhost" --port "5432" --username "postgres" --no-password --dbname "foodmart" --verbose "D:\foliveira\Ferramentas para Dashboard\Pentaho\pentaho-dashboards-examples\foodmart.backup"

Start:
C:\Program Files\PostgreSQL\9.6\bin>pg_ctl -D "C:\Program Files\PostgreSQL\9.6\data" start

Stop:
C:\Program Files\PostgreSQL\9.6\bin>pg_ctl -D "C:\Program Files\PostgreSQL\9.6\data" stop

== INI ==

Size do BD Oracle
select
"Reserved_Space(MB)", "Reserved_Space(MB)" - "Free_Space(MB)" "Used_Space(MB)","Free_Space(MB)"
from(
select
(select sum(bytes/(1014*1024)) from dba_data_files) "Reserved_Space(MB)",
(select sum(bytes/(1024*1024)) from dba_free_space) "Free_Space(MB)"
from dual );

Reserved_Space(MB) Used_Space(MB) Free_Space(MB)
------------------ -------------- --------------
        1666,27219     1066,39719        599,875

== FIM ==

== FIM ==

== INI ==

Alteração da porta HTTP do Oracle:

Exec DBMS_XDB.SETHTTPPORT(8088);

== FIM ==

== INI ==

Usuário e senha de admin do WebLogic

Usuário: weblogic
Senha: Admin123

== FIM ==

== INI ==

Start/Stop WebLogic:

https://helpx.adobe.com/br/experience-manager/6-3/forms/using/admin-help/starting-stopping-weblogic-server.html

== FIM ==

== INI ==


== FIM ==

== INI ==

Adicionar datasource no WildFly:

Execute o script ./jboss-cli.sh.
Porta 8080: ./jboss-cli.sh --connect --controller=localhost:9990
Porta 8180: ./jboss-cli.sh --connect --controller=localhost:10090
Entre com os seguintes comandos:
connect
Oracle:
/subsystem=datasources/jdbc-driver=ojdbc7:add(driver-name=ojdbc7,driver-module-name=oracle.jdbc.driver,driver-xa-datasource-class-name=oracle.jdbc.xa.client.OracleXADataSource)

== FIM ==

Comandos SQL

ALTER TABLE table_name  RENAME TO new_table_name;

== INI ==

Comando sp_who2

DECLARE @Table TABLE(
        SPID INT,
        Status VARCHAR(MAX),
        LOGIN VARCHAR(MAX),
        HostName VARCHAR(MAX),
        BlkBy VARCHAR(MAX),
        DBName VARCHAR(MAX),
        Command VARCHAR(MAX),
        CPUTime INT,
        DiskIO INT,
        LastBatch VARCHAR(MAX),
        ProgramName VARCHAR(MAX),
        SPID_1 INT,
        REQUESTID INT
)

INSERT INTO @Table EXEC sp_who2

SELECT  *
FROM    @Table
WHERE DBName = 'DWMYHONDAPRD';



== FIM ==

URLs e drivers JDBC

SQL Server:
URL: jdbc:sqlserver://10.148.202.224:1433;DatabaseName=SAHSADQQAS;SelectedMethod=Cursor
Driver: com.microsoft.sqlserver.jdbc.SQLServerDriver

JTDS:
URL: jdbc:jtds:sqlserver://SRVCCAA:1433;databaseName=CCAA_MDM;SelectMethod=cursor
Driver: net.sourceforge.jtds.jdbc.Driver

PostgreSQL:
URL: jdbc:postgresql://dbmsl01:5432/eou@.'\"*+=|][(){}$&!#%/:,;
Driver: org.postgresql.Driver

Oracle:
URL: 
Driver: oracle.jdbc.driver.OracleDriver

MySQL:
URL: jdbc:mysql://localhost:3306/fkn_identity
Driver: com.mysql.jdbc.Driver


##  Comandos Linux e Windows

Linux

Aplica dos2unix recursivamente no diretorio {dir}:
find {dir} -type f -print0 | xargs -0 dos2unix

G-zip
Compactação:
tar -vczf arquivo.tar.gz diretorio

Extração:
tar -vxzf arquivo.tar.gz

Charset de arquivo:
file -I arquivo.txt
arquivo.txt: text/plain; charset=iso-8859-1

Verificar espaço em disco no Linux:
df -hs

Conversão de encode:
iconv -f iso-8859-1 -t utf-8 arquivo.txt > arquivo_novo.txt

IPs de um DNS:
nslookup <dns>

Comando curl para requisição HTTP POST:
curl -H "Content-Type: application/json" -X POST -d '{"nomCliente": "ANTONIA ANGELA DE ASSIS", "tipoPessoa": "FIS", "numCpfCnpj": "5556732272", "dscEmail": "teste@teste.com"}' http://10.40.11.14:8280/CustomerHSF/retrieveCustomerHSF

Tamanho de arquivo:
myfilesize=$(du -b arquivo.txt | cut -f1)
echo $myfilesize

Windows

Copiar arquivos/pastas de D:\ para W:\ :
robocopy D:\ W:\ /e /r:1 /w:1

== INI ==

Executar script sem sair do CMD
cmd /k script.bat

== FIM ==

Limpar o cache DNS:
ipconfig /flushdns

== INI ==

## Referências de linguagens de programação

Linguagem C:
http://www.cplusplus.com/reference/clibrary/

Linguagem Java:
https://docs.oracle.com/en/java/javase/index.html

Linguagem JavaScript:
https://developer.mozilla.org/en-US/docs/Web/JavaScript
