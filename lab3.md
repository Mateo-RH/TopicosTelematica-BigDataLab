# 3. Hive y Sqoop

## Hive

Para realizar los ejercicios de hive se utilizan una serie de scripts SQL para la creacion de la base de datos y posteriormente las tablas y aprovisionamiento de estas.
todos estos querys los almacene y les saque un screenshot que encontraran a continuacion con su respectiva descripcion.

[Saved Querys](savedQuerys.md)

### Join con Hive

El siguiente query realiza un join entre las tablas _EXPO_ y _HDI_

![joinExpoHdi.JPG](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/savedQuerys/joinExpoHdi.JPG?raw=true)

[Output](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/tree/master/documentos/join_expo_hdi.csv)

### Wordcount con Hive

Ahora realizaremos el ejercicio del wordcount, primero por palabra y luego por frequencia.

**ordenado por palabra**

![docsWordOrder.JPG](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/savedQuerys/docsWordOrder.JPG?raw=true)

[Output](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/tree/master/documentos/docs-wordcound-wordOrder.csv)

**ordenado por frequencia de menor a mayor**

![docsFrequency.JPG](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/savedQuerys/docsFrequency.JPG?raw=true)

[Output](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/tree/master/documentos/docs-wordcount-frequencyOrder.csv)

### Reto

## Sqoop

Para esta parte del laboratorio es necesario primero crear una base de datos MySQL en _AWS RDS_ y alli crear una serie de tablas y aprovisionarlas.

para conectarme a la base de datos utilice una instancia _EC2_ donde instale _mysql_.
A continuacion la conexion con rds y creacion/aprovisionamiento de _cursodb_ y _retaildb_

![cursodb](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/lab3/cursodb.png?raw=true)

Como parte del ejercicio tambien hice pruebas para calcular resultados, como el salario de los empleados.

![mysqlAVG.PNG](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/lab3/mysqlAVG.PNG?raw=true)

Tambien es necesario realizar la siguiente configuracion para poder utilizar los comandos de Sqoop desde Hue, sin embargo a pesar de realizar esta configuracion, finalmente termine ejecutando la mayoria de los comandos de sqoop desde la consola

![sqoopConfiguracion](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/lab3/configuracion_sqoop.png?raw=true)

Transfiriendo los datos desde mysql a hdfs con sqoop

![sqoop-transferir.PNG](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/lab3/sqoop-transferir.PNG?raw=true)

Creacion de una tabla en hive con la estructura de una tabla existente en mysql.
Para este ejercicio me toco crear la base de datos _mydbhive_ previamente desde hive en hue

![sqoop-import.PNG](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/lab3/sqoop-import.PNG?raw=true)

Transfiriendo los datos de mysql a la tabla en hive

![sqoop-fillDB.PNG](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/lab3/sqoop-fillDB.PNG?raw=true)

Los comandos restantes del laboratorio son para experimentar mas interacciones entre mysql y sqoop, a continuacion dejare algunos de los que se utilizaron en el laboratorio

```

sqoop import-all-tables --connect jdbc:mysql://mysqldb.cavef8jzeaek.us-east-1.rds.amazonaws.com:3306/retail_db --username=retail_dba --password=retail_dba --warehouse-dir /tmp/mysqlOut1 --mysql-delimiters -m 1

sqoop import-all-tables --connect jdbc:mysql://mysqldb.cavef8jzeaek.us-east-1.rds.amazonaws.com:3306/retail_db --username=retail_dba --password=retail_dba --warehouse-dir=/tmp/mysqlOut1 --hive-import --mysql-delimiters -m 1 

sqoop import-all-tables --connect jdbc:mysql://mysqldb.cavef8jzeaek.us-east-1.rds.amazonaws.com:3306/retail_db --username=retail_dba --password=retail_dba --hive-database mydbhive --create-hive-table --warehouse-dir=/tmp/mysqlOut1 --hive-import --mysql-delimiters -m 1 

sqoop import-all-tables --connect jdbc:mysql://mysqldb.cavef8jzeaek.us-east-1.rds.amazonaws.com:3306/retail_db --username=retail_dba --password=retail_dba --hive-database mydbhive --hive-overwrite --warehouse-dir=/tmp/mysqlOut1 --hive-import --mysql-delimiters -m 1 
```
Lo unico que se debe tener en cuenta para estos comandos es cambiar el link de la base de datos mysql que se esta utilizando.

### Case retal DB

* Primero creo la base de datos retail_db en hive
```
create database retail_db;
```

* Luego importo los datos de mysql via sqoop
```
sqoop import-all-tables --connect jdbc:mysql://mysqldb.cavef8jzeaek.us-east-1.rds.amazonaws.com:3306/retail_db --username=retail_dba --password=retail_dba --hive-database retail_db --hive-overwrite --hive-import --warehouse-dir=/tmp/retail_dbtmp -m 1 --mysql-delimiters
```

![caseRetailDB1.PNG](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/lab3/caseRetailDB1.PNG?raw=true)

* Obtener categorias mas populares de productos
```
SELECT c.category_name, count(order_item_quantity) as count
FROM order_items oi
inner join products p on oi.order_item_product_id = p.product_id
inner join categories c on c.category_id = p.product_category_id
group by c.category_name
order by count desc
limit 10
```

[Output](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/tree/master/documentos/caseRetailDBOutput1.xlsx)

* Obtener top 10 de productos que generan ganancias
```
SELECT p.product_id, p.product_name, r.revenue
FROM products p inner join
(select oi.order_item_product_id, sum(cast(oi.order_item_subtotal as float)) as revenue
from order_items oi inner join orders o
on oi.order_item_order_id = o.order_id
where o.order_status <> 'CANCELED'
and o.order_status <> 'SUSPECTED_FRAUD'
group by order_item_product_id) r
on p.product_id = r.order_item_product_id
order by r.revenue desc
limit 10
```

[Output](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/tree/master/documentos/caseRetailDBOutput2.xlsx)

* Subo los logs al HDFS
```
hdfs dfs -put datasets/retail_logs/access.log /user/admin/datasets/retail_logs/

USE admin;
CREATE EXTERNAL TABLE tmp_access_logs (
        ip STRING,
        fecha STRING,
        method STRING,
        url STRING,
        http_version STRING,
        code1 STRING,
        code2 STRING,
        dash STRING,
        user_agent STRING)
    ROW FORMAT SERDE 'org.apache.hadoop.hive.contrib.serde2.RegexSerDe'
    WITH SERDEPROPERTIES (
        'input.regex' = '([^ ]*) - - \\[([^\\]]*)\\] "([^\ ]*) ([^\ ]*) ([^\ ]*)" (\\d*) (\\d*) "([^"]*)" "([^"]*)"',
        'output.format.string' = "%1$$s %2$$s %3$$s %4$$s %5$$s %6$$s %7$$s %8$$s %9$$s")
    LOCATION '/user/admin/datasets/retail_logs/';

hdfs dfs -mkdir /user/admin/warehouse/access_logs_etl
```

* Creo directorio para la tabla externa con _ETL_
```
    CREATE EXTERNAL TABLE etl_access_logs (
        ip STRING,
        fecha STRING,
        method STRING,
        url STRING,
        http_version STRING,
        code1 STRING,
        code2 STRING,
        dash STRING,
        user_agent STRING)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ','
    LOCATION '/user/admin/warehouse/access_logs_etl/';
```

* Directorios creados en hdfs

![caseRetailDB3.PNG](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/lab3/caseRetailDB3.PNG?raw=true)

* Evidencias de Querys

![caseRetailDB2.PNG](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/lab3/caseRetailDB2.PNG?raw=true)



[volver](index.md)
