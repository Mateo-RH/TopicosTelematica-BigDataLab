
# 2. Laboratorio Map/Reduce

## MyPC

Para ejecutar el [wordcount-local.py](https://github.com/st0263eafit/bigdata/blob/master/02-mapreduce/wordcount-local.py) y [wordcount-mr.py](https://github.com/st0263eafit/bigdata/blob/master/02-mapreduce/wordcount-mr.py) en mi computador primero instale Python, pip y mrjob.
1. [Instalacion de python](https://github.com/BurntSushi/nfldb/wiki/Python-&-pip-Windows-installation)
2. Despues de instalar python y pip, ejecutar la siguiente instruccion en la terminal: ``` pip install mrjob``` 

**Corriendo el wordcount**
![pc.JPG](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/labs/pc.JPG?raw=true)

**Output Files**
* [local](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/labs/wordcount-local-output.txt)
* [mr](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/labs/wordcount-mr-output.txt)

## DCA/Jupyter

El DCA ya tenia las herramientas neesarias para realizar el ejercicio, por lo que solo fue necesario conectarme y ejecutar los scripts en una terminal de jupyter

**Corriendo el wordcount**
1. Sin Map Reduce

![sinMapReduce.JPG](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/local/sinMapReduce.JPG?raw=true)

2. Con Map Reduce

![conMapReduce.JPG](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/local/conMapReduce.JPG?raw=true)

## EMR

Para realizar el mismo ejercicio en el EMR de aws, primero fue necesario completar los siguientes pasos:
1. conectarme al nodo master del cluster: ```ssh -i "cluster.pem" hadoop@ec2-18-212-42-209.compute-1.amazonaws.com```
2. instalar git: ```sudo yum install -y git```
3. descargar el repositorio ``` git clone https://github.com/st0263eafit/bigdata.git ```
3. instalar mrjob: ```sudo pip install mrjob```

**Corriendo el wordcount**
1. Sin Map Reduce

![emr-local.JPG](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/labs/emr-local.JPG?raw=true)

2. Con Map Reduce

![emr-mr.JPG](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/labs/emr-mr.JPG?raw=true)

## Ejercicio 1

1. El salario promedio por Sector Económico (SE)

**codigo**

![punto1.JPG](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/labs/punto1.JPG?raw=true)

**resultado**

![punto1.JPG](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/labs/punto1_res.JPG?raw=true)

2. El salario promedio por Empleado

**codigo**

![punto1.JPG](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/labs/punto2.JPG?raw=true)

**resultado**

![punto1.JPG](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/labs/punto2_res.JPG?raw=true)

3. Número de SE por Empleado que ha tenido a lo largo de la estadística

**codigo**

![punto1.JPG](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/labs/punto3.JPG?raw=true)

**resultado**

![punto1.JPG](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/labs/punto3_res.JPG?raw=true)

