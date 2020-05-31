# Procedimentos

Procedimentos gerais e referencias sobre scripts/comandos Windows/Linux, gerenciamento de BDs, programação, entre outros

## Gerenciamento do banco de dados

**MySQL**

* Iniciar (Windows): `` mysqld --defaults-file="C:\ProgramData\MySQL\MySQL Server 5.7\my.ini" --console ``
* Parar: `` mysqladmin -u root -p shutdown ``
* Backup: `` mysqldump -h <host> -u <usuario> -p <banco> --routines --events > <backup>.sql ``
* Restore: `` mysql -h <host> -u <usuario> -P <porta> -p --protocol=TCP < <backup>.sql ``

* Criar banco: `` CREATE DATABASE <banco>; ``
* Criar usuário: `` CREATE USER '<usuario>'@'%' IDENTIFIED BY '<senha>'; `` 
* Privilégios para o usuário: `` GRANT ALL PRIVILEGES ON <banco>.* TO '<usuario>'@'%'; FLUSH PRIVILEGES; ``
* Login no banco: `` mysql -h <host> -u <usuario> -P <porta> -p --protocol=TCP <banco> ``

**PostgreSQL**

* Iniciar: `` C:\Program Files\PostgreSQL\9.6\bin>pg_ctl -D "C:\Program Files\PostgreSQL\9.6\data" start ``
* Parar: `` C:\Program Files\PostgreSQL\9.6\bin>pg_ctl -D "C:\Program Files\PostgreSQL\9.6\data" stop ``
* Backup: `` "C:\Program Files\PostgreSQL\9.6\bin\pg_dump.exe" --file "D:\\foliveira\\Ferramentas para Dashboard\\Pentaho\\pentaho-dashboards-examples\\pentaho_cde_demo.sql" --host "localhost" --port "5432" --username "postgres" --no-password --verbose --format=p "pentaho_cde_demo" ``
* Restore: `` "C:\Program Files\PostgreSQL\9.6\bin\pg_restore.exe" --host "localhost" --port "5432" --username "postgres" --no-password --dbname "foodmart" --verbose "D:\foliveira\Ferramentas para Dashboard\Pentaho\pentaho-dashboards-examples\foodmart.backup" ``

**MongoDB**

* Backup: `` mongodump --host localhost --port 27017 --authenticationDatabase datacare --collection relatorio --db datacare --out D:\Assesso\backup\mongodump201811281059 ``
* Login no banco: `` mongo --username datacare_dev --password --authenticationDatabase datacare_dev --host localhost --port 27017 ``
* Remover coleção: db.collection.remove({})

**SQL Server**

**Oracle**


== INI ==

Oracle

BEGIN
  -- Disable the web interface
  DBMS_XDB.SETHTTPPORT(0);
  -- Disable FTP just in case
  DBMS_XDB.SETFTPPORT(0);
END;
== FIM ==

== INI ==
MySQL

indices de uma tabela:
show index from <table>;

variaveis:
SHOW VARIABLES LIKE '%timeout%';

tabelas em uso:
show open tables where in_use > 0;

== FIM ==

== INI ==

Alterar senha do usuário administrador do banco de dados

MySQL:
mysqladmin -u root -p<OLDPASSWORD> password <NEWPASSWORD>

== FIM ==

== INI ==

Versao do Oracle:
SELECT * FROM V$VERSION;

== FIM ==

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



== INI ==

SQL Server:

Listagem das tabelas:
SELECT name FROM dbo.sysobjects WHERE type = 'U';

Listagem das procedures:
SELECT name FROM dbo.sysobjects WHERE type = 'P';

Schema das tabelas:
SELECT * FROM INFORMATION_SCHEMA.TABLES;
TABLE_CATALOG	TABLE_SCHEMA	TABLE_NAME	TABLE_TYPE
BD-DCARE-DEV01	dbo	TBDCAGD_ETAPA_PROCESSO	BASE TABLE

Schema das procedures:
SELECT * FROM INFORMATION_SCHEMA.ROUTINES;

Oracle:

SELECT table_name  from all_tables where owner = 'DATACARE';
SELECT object_name  from all_procedures where owner = 'DATACARE';



== FIM ==

== INI ==

Owner dos objetos

Oracle:
SELECT TABLE_NAME, OWNER FROM ALL_TABLES;
SELECT OBJECT_NAME, OWNER FROM ALL_PROCEDURES;
SELECT SEQUENCE_NAME, SEQUENCE_OWNER FROM ALL_SEQUENCES;

== FIM ==

== INI ==

Configura o NOCOUNT no banco SQL Server:

-- CONFIGURA ONCOUNT = ON
EXEC sys.sp_configure'user options','512'
RECONFIGURE

-- CONFIGURA ONCOUNT = OFF
EXEC sys.sp_configure'user options','0'
RECONFIGURE

-- RUN_VALUE = 0   => ONCOUNT = OFF
-- RUN_VALUE = 512 => ONCOUNT = ON
EXEC sys.sp_configure'user options';

== INI ==

Conectar no banco Oracle via SQLPLUS no Windows:

sqlplus DTCPJUSER/DTCPJUSER@'(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(Host=dbmsl01)(Port=1521))(CONNECT_DATA=(SERVICE_NAME=XE)))'

sqlplus system@'(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(Host=localhost)(Port=1521))(CONNECT_DATA=(SERVICE_NAME=XE)))'

== FIM ==

== INI ==

Oracle - Imprimir variavel na saida:

SET SERVEROUTPUT ON;
DECLARE 
  VARIAVEL NUMERIC(10);
BEGIN

dbms_output.put_line('Franklin' || ' de ' || 'Oliveira');

COMMIT;
END;
/

Exemplo:

SET SERVEROUTPUT ON;
DECLARE 
  v_MAX_ID_COLUNA NUMERIC(10);
BEGIN
SELECT NVL(MAX(ID_COLUNA),0) + 1 INTO v_MAX_ID_COLUNA FROM TABELA;
dbms_output.put_line('Franklin' || v_MAX_ID_COLUNA);

COMMIT;
END;
/


== FIM ==

== INI ==

Encoding banco Oracle:

Windows:
set NLS_LANG=American_America.WE8ISO8859P1​

Linux / Unix:
export NLS_LANG=American_America.WE8ISO8859P1​

Ref.:
http://www.orafaq.com/wiki/NLS_LANG

== FIM ==


== INI ==

SQL Server:

-- disable all constraints and triggers
EXEC sp_MSforeachtable "ALTER TABLE ? NOCHECK CONSTRAINT all"
EXEC sp_MSforeachtable "ALTER TABLE ? DISABLE TRIGGER all"

-- enable all constraints and triggers
EXEC sp_MSforeachtable @command1="print '?'", @command2="ALTER TABLE ? CHECK CONSTRAINT all"
EXEC sp_MSforeachtable @command1="print '?'", @command2="ALTER TABLE ? ENABLE TRIGGER  all"

== FIM ==

== INI ==

Execucao de scripts:

Oracle:
sqlplus <user>@'(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(Host=<host>)(Port=<port>))(CONNECT_DATA=(SERVICE_NAME=<sid>)))'

SQL Server:
SQLCMD -S <host>\<instancia>,<port> -U <user> -d <database> -i script.sql -o execucao.log

MySQL:
mysql -h <host> -u <user> -p <database> -v --default-character-set=latin1 < script.sql > execucao.log

== FIM ==

== INI ==

ALTER USER <user> IDENTIFIED BY <new_password>

== FIM ==


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

Terminador de linha:
Linux: cat -A <arquivo>
Windows: 

== FIM ==

== INI ==
Cópia remota de arquivos:
scp -rp /tmp/diretorio@<host-remoto>:/tmp
== FIM ==

== INI ==

Verificação da versão do Linux (32 ou 64 bits):

arch

32-bit ("i686" or "i386")
64-bit ("x86_64")

Verificação da versão do Windows (32 ou 64 bits):

wmic OS get OSArchitecture

== FIM ==

== INI ==

Help de comandos

Exemplos:

linux:
cd --help

windows:
help dir

== FIM ==


== INI ==

systemctl -t service
sudo journalctl -u datacare-executor-prd
systemctl status <nome servico>.service

== FIM ==

== INI ==

Localização dos arquivos de configuração dos serviços:
/etc/systemd/system/

== FIM ==



== INI ==

Comparação de arquivos no Windows:

FC arquivo1.txt arquivo2.txt

Comparação de arquivos no Linux:

diff arquivo1.txt arquivo2.txt

== FIM ==

== INI ==

Espaço em disco: WinDirStat

== FIM ==

== INI ==

Informações do SO linux:
lsb_release -a
cat /etc/os-release
hostnamectl

== FIM ==

== INI ==

Localização do Java

Windows:
where java

== FIM ==

== INI ==

Mémória disponível:
free -m

== FIM ==

== INI ==

uptime

== FIM ==

== INI ==

Versão do Java:

java -d32 -version
java -d64 -version

== FIM ==

== INI ==

Portas em uso:
netstat -anp | grep 8787

PID na última coluna

== FIM ==


## Referências de linguagens de programação

Linguagem C:
http://www.cplusplus.com/reference/clibrary/

Linguagem Java:
https://docs.oracle.com/en/java/javase/index.html

Linguagem JavaScript:
https://developer.mozilla.org/en-US/docs/Web/JavaScript

# Categorizar

- Consumir API REST/SOAP - Pesquisar servico online

== INI ==

Apagar conteúdo de arquivo:

break > arquivo.txt

== FIM ==

== INI ==

Analisar simbolos:
Comando: objdump

== FIM ==

== INI ==
Simbolos de um .so:
nm -g arquivo.so

== FIM ==

== INI ==

Java Decompiler:
http://jd.benow.ca/

== FIM ==

== INI ==

== INI ==

Estrutura WSDL

<wsdl:definitions>
    <wsdl:types>...</wsdl:types>
    <wsdl:message>...</wsdl:message>
    <wsdl:portType>...</wsdl:portType>
    <wsdl:binding>...</wsdl:binding>
    <wsdl:service>...</wsdl:service>
</wsdl:definitions>

Relações:

<wsdl:service> ==> <wsdl:binding> ==> <wsdl:portType>  ==> <wsdl:message>   ⇒ <wsdl:message>

== FIM ==


== FIM ==

== INI ==

WildFly - habilitar log das requisicoes:

<subsystem xmlns="urn:jboss:domain:undertow:3.1">
            <buffer-cache name="default"/>
            <server name="default-server">
                <http-listener name="default" socket-binding="http" max-parameters="10000" redirect-socket="https" enable-http2="true"/>
                <https-listener name="https" socket-binding="https" security-realm="ApplicationRealm" enable-http2="true"/>
                <host name="default-host" alias="localhost">
                    <location name="/" handler="welcome-content"/>
                    <filter-ref name="server-header"/>
                    <filter-ref name="x-powered-by-header"/>
                    <filter-ref name="request-dumper"/>
                </host>
            </server>
            <servlet-container name="default">
                <jsp-config/>
                <websockets/>
            </servlet-container>
            <handlers>
                <file name="welcome-content" path="${jboss.home.dir}/welcome-content"/>
            </handlers>
            <filters>
                <response-header name="server-header" header-name="Server" header-value="WildFly/10"/>
                <response-header name="x-powered-by-header" header-name="X-Powered-By" header-value="Undertow/1"/>
                <filter name="request-dumper" class-name="io.undertow.server.handlers.RequestDumpingHandler" module="io.undertow.core"/>
            </filters>
        </subsystem>

== FIM ==
