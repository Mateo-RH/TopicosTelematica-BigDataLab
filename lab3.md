# 3. Hive y Sqoop

## Hive

Para realizar los ejercicios de hive se utilizan una serie de scripts SQL para la creacion de la base de datos y posteriormente las tablas y aprovisionamiento de estas.
todos estos querys los almacene y les saque un screenshot que encontraran a continuacion con su respectiva descripcion.

[Saved Querys](savedQuerys.md)

### Join con Hive

El siguiente query realiza un join entre las tablas _EXPO_ y _HDI_

![joinExpoHdi.JPG](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/savedQuerys/joinExpoHdi.JPG?raw=true)

[Output](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/queryOutputs/join_expo_hdi.csv)

### Wordcount con Hive

Ahora realizaremos el ejercicio del wordcount, primero por palabra y luego por frequencia.

**ordenado por palabra**

![docsWordOrder.JPG](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/savedQuerys/docsWordOrder.JPG?raw=true)

[Output](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/queryOutputs/docs-wordcound-wordOrder.csv)

**ordenado por frequencia de menor a mayor**

![docsFrequency.JPG](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/savedQuerys/docsFrequency.JPG?raw=true)

[Output](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/queryOutputs/docs-wordcount-frequencyOrder.csv)

### Reto

## Sqoop

Para esta parte del laboratorio es necesario primero crear una base de datos MySQL en _AWS RDS_ y alli crear una serie de tablas y aprovisionarlas.

para conectarme a la base de datos utilice una instancia _EC2_ donde instale _mysql_.
A continuacion la instalaion de mysql, conexion con rds y creacion/aprovisionamiento de _cursodb_

![cursodb](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/lab3/cursodb.png?raw=true)

Tambien es necesario realizar la siguiente configuracion para poder utilizar los comandos de Sqoop desde Hue

![sqoopConfiguracion](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/lab3/configuracion_sqoop.png?raw=true)

[volver](index.md)
