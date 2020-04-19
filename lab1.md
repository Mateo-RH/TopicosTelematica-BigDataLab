# 1. Laboratorio HDFS
## EMR en el DCA

1. Descargar _dataset_ del repositorio y comprimirlo
```
git clone https://github.com/st0263eafit/bigdata.git 
cd bigdata/datasets && zip –r dataset * 
```
2. Copiar el _dataset_ al **DCA** y descomprimirlo en una carpeta
```
scp dataset.zip marami26@192.168.10.116:/home/marami26/dataset.zip 
ssh marami26@192.168.10.116 
mkdir datasets && unzip dataset.zip -d datasets 
```
3. Crear carpeta para almacenar los datasets en mi directorio de **HDFS**
```
hdfs dfs -mkdir /user/marami26/datasets 
```
4. Copiar el _dataset_ del **DCA** al directorio de **HDFS**
```
hdfs dfs –copyFromLocal datasets/* /user/marami26/datasets/ 
```

**Resultados**
* Terminal
![terminal](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/dca/terminal.png?raw=true)

* Ambari
![ambari](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/dca/ambari.png?raw=true)

## S3
Se crea un bucket en AWS S3 y se configura desbloqueando el acceso publico.
Tambien se debe de dar permisos de lectura publica a la carpeta _datasets_.

![s3](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/s3/bigdata-s3.JPG?raw=true)

## AWS EMR

1. Creamos un cluster en EMR solicitando los siguientes componentes
 * **Hadoop:** framework de bigdata con almacenamiento en el emr-5.27.0
 * **Hue:** interfaz grafica de asistencia para interactuar con el cluster
 * **Zeppelin:** notebook basado en web
 * **Sqoop:** Herramienta para transferir datos voluminosos entre _Hadoop Apache_ y bases de datos estructurales como bases de datos relacionales.
 * **Oozie:** Es un _workflow scheduler_ para administrar jobs de Apache Hadoop
 * **Hive:** _Datawarehouse_ que facilita la lectura, escritura y manejo de grandes cantidades de datos.
 * **Livy:** Es un servicio que permite la facil comunicacion con un Cluster de _Spark_ a traves de una interfaz _REST_
 * **Tez:** Marco para aplicaciones de procesamiento de datos basadas en YARN en Hadoop
 
![creacionCluster.JPG](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/cluster/creacionCluster.JPG?raw=true)

2. Habilitamos el acceso publico pero restringimos los puertos 8888 y 8890 que seran utilizados para _Hue_ y _Zeppelin_

![publicAccess.JPG](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/cluster/publicAccess.JPG?raw=true)

3. Configuramos el grupo de seguridad del master para exponer los puertos 8888 y 8890

![secGroups.JPG](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/cluster/secGroups.JPG?raw=true)

4. Para poder clonar este cluster damos click en la opcion _Exportación de la CLI de AWS_

![recreacion.JPG](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/cluster/recreacion.JPG?raw=true)

5. Recreacion del cluster con AWS CLI
```
aws emr create-cluster --auto-scaling-role EMR_AutoScaling_DefaultRole --applications Name=Hadoop Name=Hive Name=Hue Name=Spark Name=Zeppelin Name=Tez Name=Sqoop Name=Oozie Name=Livy --ebs-root-volume-size 10 --ec2-attributes '{"KeyName":"cluster","InstanceProfile":"EMR_EC2_DefaultRole","SubnetId":"subnet-08c32029","EmrManagedSlaveSecurityGroup":"sg-00bebe09e6bbb50af","EmrManagedMasterSecurityGroup":"sg-08fdf4754b70c288a"}' --service-role EMR_DefaultRole --enable-debugging --release-label emr-5.27.0 --log-uri 's3n://aws-logs-242641527932-us-east-1/elasticmapreduce/' --name 'MiClusterEMR' --instance-groups '[{"InstanceCount":2,"EbsConfiguration":{"EbsBlockDeviceConfigs":[{"VolumeSpecification":{"SizeInGB":32,"VolumeType":"gp2"},"VolumesPerInstance":2}]},"InstanceGroupType":"CORE","InstanceType":"m4.xlarge","Name":"Principal - 2"},{"InstanceCount":1,"EbsConfiguration":{"EbsBlockDeviceConfigs":[{"VolumeSpecification":{"SizeInGB":32,"VolumeType":"gp2"},"VolumesPerInstance":2}]},"InstanceGroupType":"MASTER","InstanceType":"m4.xlarge","Name":"Maestro - 1"}]' --scale-down-behavior TERMINATE_AT_TASK_COMPLETION --region us-east-1
```

6. Eliminacion del cluster con AWS CLI
```
aws emr terminate-clusters --cluster-ids <clusterID>
```

**Resultados**

* **Hue**
![hue.JPG](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/cluster/hue.JPG?raw=true)

* **Zeppelin**
![zeppelin.JPG](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/cluster/zeppelin.JPG?raw=true)

* **SSH**
![ssh-conection.JPG](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/cluster/ssh-conection.JPG?raw=true)

## Hue

#### HDFS

1. En el menu hamburguesa de arriba a la izquierda seleccionamos _Files_

![hdf1.JPG](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/hue/hdf1.JPG?raw=true)

2. Ahora seleccionamos _Upload_ y subimos el _dataset_

![hdfs2.JPG](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/hue/hdfs2.JPG?raw=true)

![hdfs3.JPG](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/hue/hdfs3.JPG?raw=true)

#### S3

1. En el menu hamburguesa de arriba a la izquiera seleccionamos _S3_

![s31.JPG](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/s3/s31.JPG?raw=true)

2. A continuacion veremos los _Buckets_ de S3 que poseemos en la cuenta

![s32.JPG](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/s3/s32.JPG?raw=true)

3. Al seleccionar el Bucket creado previamente, tendremos acceso a el dataset que cargamos alli.

![s33.JPG](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/s3/s33.JPG?raw=true)


[volver](index.md)
