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

[volver](index.md)
