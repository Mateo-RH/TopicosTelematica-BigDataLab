# Proyecto big data

## Autores
![fantasma](https://raw.githubusercontent.com/Mateo-RH/TopicosTelematica-BigDataLab/master/imagenes/trabajo3/sexyFantasma.jpg)

_Juan Camilo Echeverri Salazar_



![RH](https://raw.githubusercontent.com/Mateo-RH/TopicosTelematica-BigDataLab/master/imagenes/trabajo3/matejobs.jpg)

_Mateo Ramirez Hernandez_



### Descripción

Proyecto 3 para la materia topicos de telematica.
la actividad planteada se describe en el siguiente [link](https://github.com/st0263eafit/bigdata/blob/master/trabajo3-spark-covid19.md).

### Proposito 

Realizar el ejercicio planteado por el profesor, donde se pueda evidenciar el ciclo de vida de big data (Fuente, Ingesta, Procesamiento, Aplicaciones)

**1. Fuente** Los datos fueron adquiridos de los siguientes links: 
 
 * [DataSet global](https://data.humdata.org/dataset/novel-coronavirus-2019-ncov-cases) 
 * [DataSet Colombia 1](https://data.humdata.org/dataset/positive-cases-of-covid-19-in-colombia) 
 * [DataSet Colombia 2](https://www.ins.gov.co/Paginas/Inicio.aspx)
 
**2. Ingesta** 
Los datos adquiridos se almacenaron en un bucket S3 de amazon
*IMAGEN DEL BUCKET*

**3. Procesamiento** 
Para el procesamiento se creo un cluster EMR en amazon
*imagen cluster*

luego creamos un notebook de jupyter asociado a dicho cluster
*ïmagen notebook*

En el notebook realizamos todo el procesamiento utilizando PySpark.
La documentacion completa del procesamiento se encuentra en el siguiente [link](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/documentos/trabajo3.ipynb)

**4. Aplicacion**

Despues de realizar el procesamiento de datos exportamos dos nuevos Datasets los cuales son el resultado del procesamiento previo.

* [gobal.csv](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/documentos/global.csv)
* [colombia.csv](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/documentos/colombia.csv)

Para el desarrollo de la aplicacion utilizamos el software [Tableu](https://www.tableau.com/es-es).



[volver](index.md)
