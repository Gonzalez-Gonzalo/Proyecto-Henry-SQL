# Proyecto-Henry-SQL



En el ámbito de la manipulación de grandes volúmenes de datos, la gestión eficiente de bases de datos, como MySQL, puede volverse laboriosa. 
Por esta razón, se considera viable la adopción de Docker como herramienta alternativa.
Docker proporciona una solución efectiva para el manejo de big data a través del empleo de contenedores, los cuales encapsulan imágenes que 
facilitan la transferencia de información entre diversos servidores. Este enfoque de contenerización optimiza la portabilidad y la eficiencia en la 
gestión de datos a escala.
El concepto de big data ostenta una relevancia fundamental en las corporaciones de gran envergadura, haciendo hincapié en los tres principios 
fundamentales conocidos como las "3V": velocidad, volumen y variedad. Estos elementos constituyen pilares esenciales para comprender y abordar los 
retos inherentes a la gestión de conjuntos masivos de datos en entornos empresariales de gran complejidad.

En la practica integradora nos solicitan realizar la configuracion sobre una Maquina Virtual Linux, en la cuales comenzaremos con clonar el 
directorio propuesto por el proyecto https://github.com/soyHenry/DS-M4-Herramientas_Big_Data/tree/main, el cual nos indica que debe de ser con el 
siguiente comando git clone https://github.com/lopezdar222/herramientas_big_data, una vez realizado esto procedemos a movernos de carpeta ingresando 
en la consulta  cd herramientas_big_data, luego de ellos comenzamos con levantar todos los entornos de docker, a continuacion declaro los
respectivos comandos y sus resultados

```
adminstaller@Labo-AZ10:~/herramientas_big_data$ sudo docker-compose -f docker-compose-kafka.yml up -d
WARNING: Found orphan containers (resourcemanager, mongodb, hive-metastore-postgresql, neo4j, historyserver, zoo, spark-master, hive-server, zeppelin, hbase-regionserver, nodemanager, datanode, hive-metastore, spark-worker-1, namenode, hbase-master) for this project. If you removed or renamed this service in your compose file, you can run this command with the --remove-orphans flag to clean it up.
zookeeper_container is up-to-date
kafka_container is up-to-date
kafka_manager is up-to-date
```
```
adminstaller@Labo-AZ10:~/herramientas_big_data$ sudo docker-compose -f docker-compose-v4.yml up -d
WARNING: Found orphan containers (neo4j, hive-metastore-postgresql, zeppelin, hive-metastore, hive-server, zookeeper_container, hbase-master, kafka_container, zoo, mongodb, hbase-regionserver, kafka_manager) for this project. If you removed or renamed this service in your compose file, you can run this command with the --remove-orphans flag to clean it up.
historyserver is up-to-date
datanode is up-to-date
namenode is up-to-date
resourcemanager is up-to-date
nodemanager is up-to-date
spark-master is up-to-date
spark-worker-1 is up-to-date
```
```
adminstaller@Labo-AZ10:~/herramientas_big_data$ sudo docker-compose -f docker-compose-v3.yml up -d
WARNING: Found orphan containers (kafka_container, zookeeper_container, spark-master, spark-worker-1, kafka_manager) for this project. If you removed or renamed this service in your compose file, you can run this command with the --remove-orphans flag to clean it up.
hive-metastore-postgresql is up-to-date
hbase-master is up-to-date
resourcemanager is up-to-date
mongodb is up-to-date
Starting zoo ...
neo4j is up-to-date
hive-metastore is up-to-date
hbase-regionserver is up-to-date
zeppelin is up-to-date
nodemanager is up-to-date
historyserver is up-to-date
namenode is up-to-date
datanode is up-to-date
hive-server is up-to-date
Starting zoo ... error

ERROR: for zoo  Cannot start service zoo: driver failed programming external connectivity on endpoint zoo (4e95cc3b2aa7d847f38224e5afe87f82cc0a982b93aae89e42c9249ae1cc1223): Bind for 0.0.0.0:2181 failed: port is already allocated

ERROR: for zoo  Cannot start service zoo: driver failed programming external connectivity on endpoint zoo (4e95cc3b2aa7d847f38224e5afe87f82cc0a982b93aae89e42c9249ae1cc1223): Bind for 0.0.0.0:2181 failed: port is already allocated
ERROR: Encountered errors while bringing up the project.
```
En este punto noto que al intentar iniciar el entorno zookeeper_container este falla al estar siendo ocupado por el comando anterior, es decir 
sudo docker-compose -f docker-compose-kafka.yml up -d, proceso a bajar dicho entorno buscando el id con el comando sudo docker ps, una vez 
identificado el id ejecuto sudo docker stop {ID}, continuo con la ejecucion.
```
adminstaller@Labo-AZ10:~/herramientas_big_data$ sudo docker-compose -f docker-compose-v2.yml up -d
WARNING: Found orphan containers (zoo, hbase-master, mongodb, hbase-regionserver, zookeeper_container, kafka_container, neo4j, kafka_manager, spark-master, spark-worker-1, zeppelin) for this project. If you removed or renamed this service in your compose file, you can run this command with the --remove-orphans flag to clean it up.
historyserver is up-to-date
namenode is up-to-date
hive-metastore is up-to-date
hive-metastore-postgresql is up-to-date
nodemanager is up-to-date
datanode is up-to-date
resourcemanager is up-to-date
Recreating hive-server ... done
```
y por ultimo
```
adminstaller@Labo-AZ10:~/herramientas_big_data$ sudo docker-compose -f docker-compose-v1.yml up -d
WARNING: Found orphan containers (kafka_manager, spark-master, hive-metastore-postgresql, hive-metastore, hbase-master, hbase-regionserver, neo4j, zookeeper_container, kafka_container, mongodb, spark-worker-1, hive-server, zoo, zeppelin) for this project. If you removed or renamed this service in your compose file, you can run this command with the --remove-orphans flag to clean it up.
nodemanager is up-to-date
historyserver is up-to-date
resourcemanager is up-to-date
namenode is up-to-date
datanode is up-to-date
```
una vez levantado todos los entornos propuestos contunuo con el punto numero uno

1) HDFS

Copio los archivos ubicados en la carpeta Datasets, dentro del contenedor "namenode" con los siguientes comandos
```
adminstaller@Labo-AZ10:~/herramientas_big_data$ sudo docker exec -it namenode bash
root@9b8bf947e163:/# cd home
root@9b8bf947e163:/home# mkdir Datasets
root@9b8bf947e163:/home# exit
```
Luego ejecuto la sentencia sugerida por  el redme y me encuentro con el siguiente inconveniente 
```
adminstaller@Labo-AZ10:~/herramientas_big_data$ sudo docker cp herramientas_big_data/Datasets namenode:/home/Datasets
lstat /home/adminstaller/herramientas_big_data/herramientas_big_data: no such file or directory
```
entendiendo que como ya estamos posicionados en carpeta herramientas_big_data no hace falta volverla a declarar, por ende corrijo mi sentencia y 
vuelvo a ejecutar
```
adminstaller@Labo-AZ10:~/herramientas_big_data$ sudo docker cp Datasets namenode:/home/Datasets/
Successfully copied 74.1MB to namenode:/home/Datasets/
```
me vuelvo a posicionar en el contenedor "namenode" y ejecuto
```
adminstaller@Labo-AZ10:~/herramientas_big_data$   sudo docker exec -it namenode bash
root@9b8bf947e163:/#   hdfs dfs -mkdir -p /data
root@9b8bf947e163:/#   hdfs dfs -put /home/Datasets/* /data
2023-12-10 21:38:46,392 INFO sasl.SaslDataTransferClient: SASL encryption trust check: localHostTrusted = false, remoteHostTrusted = false
2023-12-10 21:38:46,556 INFO sasl.SaslDataTransferClient: SASL encryption trust check: localHostTrusted = false, remoteHostTrusted = false
2023-12-10 21:38:46,603 INFO sasl.SaslDataTransferClient: SASL encryption trust check: localHostTrusted = false, remoteHostTrusted = false
2023-12-10 21:38:46,657 INFO sasl.SaslDataTransferClient: SASL encryption trust check: localHostTrusted = false, remoteHostTrusted = false
2023-12-10 21:38:46,712 INFO sasl.SaslDataTransferClient: SASL encryption trust check: localHostTrusted = false, remoteHostTrusted = false
2023-12-10 21:38:46,759 INFO sasl.SaslDataTransferClient: SASL encryption trust check: localHostTrusted = false, remoteHostTrusted = false
2023-12-10 21:38:46,802 INFO sasl.SaslDataTransferClient: SASL encryption trust check: localHostTrusted = false, remoteHostTrusted = false
2023-12-10 21:38:46,847 INFO sasl.SaslDataTransferClient: SASL encryption trust check: localHostTrusted = false, remoteHostTrusted = false
2023-12-10 21:38:46,930 INFO sasl.SaslDataTransferClient: SASL encryption trust check: localHostTrusted = false, remoteHostTrusted = false
2023-12-10 21:38:46,984 INFO sasl.SaslDataTransferClient: SASL encryption trust check: localHostTrusted = false, remoteHostTrusted = false
2023-12-10 21:38:47,033 INFO sasl.SaslDataTransferClient: SASL encryption trust check: localHostTrusted = false, remoteHostTrusted = false
2023-12-10 21:38:47,076 INFO sasl.SaslDataTransferClient: SASL encryption trust check: localHostTrusted = false, remoteHostTrusted = false
2023-12-10 21:38:47,126 INFO sasl.SaslDataTransferClient: SASL encryption trust check: localHostTrusted = false, remoteHostTrusted = false
2023-12-10 21:38:47,171 INFO sasl.SaslDataTransferClient: SASL encryption trust check: localHostTrusted = false, remoteHostTrusted = false
2023-12-10 21:38:51,611 INFO sasl.SaslDataTransferClient: SASL encryption trust check: localHostTrusted = false, remoteHostTrusted = false
2023-12-10 21:38:53,161 INFO sasl.SaslDataTransferClient: SASL encryption trust check: localHostTrusted = false, remoteHostTrusted = false
2023-12-10 21:38:54,163 INFO sasl.SaslDataTransferClient: SASL encryption trust check: localHostTrusted = false, remoteHostTrusted = false
2023-12-10 21:38:54,252 INFO sasl.SaslDataTransferClient: SASL encryption trust check: localHostTrusted = false, remoteHostTrusted = false
2023-12-10 21:38:54,716 INFO sasl.SaslDataTransferClient: SASL encryption trust check: localHostTrusted = false, remoteHostTrusted = false
```
Luego de realizar las tareas, no pude realizar la corroboracion propuesta en la nota dado que no pude encontrar dfs.blocksize y dfs.replication 
 por desconocer el IP del VM, lo cual uds proponen debe de ser http://<IP_Anfitrion>:9870/conf 

2) Hive

Como primer medida realizamos el paso de los archivos HQL ubicados en nuestra carpeta herramientas_big_data, nomprados como Paso02,03 y 04 
```
adminstaller@Labo-AZ10:~/herramientas_big_data$ sudo docker cp /home/adminstaller/herramientas_big_data/Paso02.hql hive-server:/home
Successfully copied 6.66kB to hive-server:/home
adminstaller@Labo-AZ10:~/herramientas_big_data$ sudo docker cp /home/adminstaller/herramientas_big_data/Paso03.hql hive-server:/home
Successfully copied 7.68kB to hive-server:/home
adminstaller@Labo-AZ10:~/herramientas_big_data$ sudo docker cp /home/adminstaller/herramientas_big_data/Paso04.hql hive-server:/home
Successfully copied 2.05kB to hive-server:/home
```
Luego creamos las Tablas en Hive. Para esto, nos ubicamos en contenedor correspondiente al servidor de Hive, y ejecutar desdea allí los scripts necesarios

```
adminstaller@Labo-AZ10:~/herramientas_big_data$   sudo docker exec -it hive-server bash
root@67bd040ac32b:/opt# hive -f /home/Paso02.hql
SLF4J: Class path contains multiple SLF4J bindings.
SLF4J: Found binding in [jar:file:/opt/hive/lib/log4j-slf4j-impl-2.6.2.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: Found binding in [jar:file:/opt/hadoop-2.7.4/share/hadoop/common/lib/slf4j-log4j12-1.7.10.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: See http://www.slf4j.org/codes.html#multiple_bindings for an explanation.
SLF4J: Actual binding is of type [org.apache.logging.slf4j.Log4jLoggerFactory]

Logging initialized using configuration in file:/opt/hive/conf/hive-log4j2.properties Async: true
OK
Time taken: 1.424 seconds
OK
Time taken: 0.029 seconds
OK
Time taken: 0.145 seconds
OK
Time taken: 0.171 seconds
OK
Time taken: 0.05 seconds
OK
Time taken: 0.046 seconds
OK
Time taken: 0.048 seconds
OK
Time taken: 0.043 seconds
OK
Time taken: 0.045 seconds
OK
Time taken: 0.037 seconds
OK
Time taken: 0.054 seconds
OK
Time taken: 0.038 seconds
OK
Time taken: 0.044 seconds
OK
Time taken: 0.051 seconds
OK
Time taken: 0.043 seconds
OK
Time taken: 0.044 seconds
OK
Time taken: 0.034 seconds
OK
Time taken: 0.029 seconds
OK
Time taken: 0.039 seconds
OK
Time taken: 0.03 seconds
OK
Time taken: 0.032 seconds
OK
Time taken: 0.028 seconds
OK
Time taken: 0.038 seconds
OK
Time taken: 0.057 seconds
root@67bd040ac32b:/opt# hive -f /home/Paso03.hql
SLF4J: Class path contains multiple SLF4J bindings.
SLF4J: Found binding in [jar:file:/opt/hive/lib/log4j-slf4j-impl-2.6.2.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: Found binding in [jar:file:/opt/hadoop-2.7.4/share/hadoop/common/lib/slf4j-log4j12-1.7.10.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: See http://www.slf4j.org/codes.html#multiple_bindings for an explanation.
SLF4J: Actual binding is of type [org.apache.logging.slf4j.Log4jLoggerFactory]

Logging initialized using configuration in file:/opt/hive/conf/hive-log4j2.properties Async: true
OK
Time taken: 2.139 seconds
OK
Time taken: 0.022 seconds
OK
Time taken: 1.225 seconds
OK
Time taken: 0.365 seconds
WARNING: Hive-on-MR is deprecated in Hive 2 and may not be available in the future versions. Consider using a different execution engine (i.e. spark, tez) or using Hive 1.X releases.
Query ID = root_20231210215931_8111a0d0-5c09-42ac-873d-253d78e7f705
Total jobs = 3
Launching Job 1 out of 3
Number of reduce tasks is set to 0 since there's no reduce operator
Job running in-process (local Hadoop)
2023-12-10 21:59:37,713 Stage-1 map = 0%,  reduce = 0%
Ended Job = job_local581045123_0001
Stage-4 is selected by condition resolver.
Stage-3 is filtered out by condition resolver.
Stage-5 is filtered out by condition resolver.
Moving data to directory hdfs://namenode:9000/data2/compra/.hive-staging_hive_2023-12-10_21-59-31_856_1656869438289168558-1/-ext-10000
Loading data to table integrador2.compra
MapReduce Jobs Launched:
Stage-Stage-1:  HDFS Read: 0 HDFS Write: 0 SUCCESS
Total MapReduce CPU Time Spent: 0 msec
OK
Time taken: 6.533 seconds
OK
Time taken: 0.121 seconds
OK
Time taken: 0.04 seconds
WARNING: Hive-on-MR is deprecated in Hive 2 and may not be available in the future versions. Consider using a different execution engine (i.e. spark, tez) or using Hive 1.X releases.
Query ID = root_20231210215938_c822ea88-787e-40e1-bc53-952dd90e88ce
Total jobs = 3
Launching Job 1 out of 3
Number of reduce tasks is set to 0 since there's no reduce operator
Job running in-process (local Hadoop)
2023-12-10 21:59:41,553 Stage-1 map = 0%,  reduce = 0%
Ended Job = job_local815876170_0002
Stage-4 is selected by condition resolver.
Stage-3 is filtered out by condition resolver.
Stage-5 is filtered out by condition resolver.
Moving data to directory hdfs://namenode:9000/data2/gasto/idtipogasto=1/.hive-staging_hive_2023-12-10_21-59-38_562_5039027691233056007-1/-ext-10000
Loading data to table integrador2.gasto partition (idtipogasto=1)
MapReduce Jobs Launched:
Stage-Stage-1:  HDFS Read: 0 HDFS Write: 0 SUCCESS
Total MapReduce CPU Time Spent: 0 msec
OK
Time taken: 3.239 seconds
WARNING: Hive-on-MR is deprecated in Hive 2 and may not be available in the future versions. Consider using a different execution engine (i.e. spark, tez) or using Hive 1.X releases.
Query ID = root_20231210215941_2cbb9b6f-aef5-4eaf-9d67-2511a8705be7
Total jobs = 3
Launching Job 1 out of 3
Number of reduce tasks is set to 0 since there's no reduce operator
Job running in-process (local Hadoop)
2023-12-10 21:59:44,303 Stage-1 map = 0%,  reduce = 0%
Ended Job = job_local915924099_0003
Stage-4 is selected by condition resolver.
Stage-3 is filtered out by condition resolver.
Stage-5 is filtered out by condition resolver.
Moving data to directory hdfs://namenode:9000/data2/gasto/idtipogasto=2/.hive-staging_hive_2023-12-10_21-59-41_809_5123374893984532733-1/-ext-10000
Loading data to table integrador2.gasto partition (idtipogasto=2)
MapReduce Jobs Launched:
Stage-Stage-1:  HDFS Read: 0 HDFS Write: 0 SUCCESS
Total MapReduce CPU Time Spent: 0 msec
OK
Time taken: 2.716 seconds
WARNING: Hive-on-MR is deprecated in Hive 2 and may not be available in the future versions. Consider using a different execution engine (i.e. spark, tez) or using Hive 1.X releases.
Query ID = root_20231210215944_e293de54-863d-41f1-acfc-f359b5a9850c
Total jobs = 3
Launching Job 1 out of 3
Number of reduce tasks is set to 0 since there's no reduce operator
Job running in-process (local Hadoop)
2023-12-10 21:59:46,388 Stage-1 map = 0%,  reduce = 0%
Ended Job = job_local864942454_0004
Stage-4 is selected by condition resolver.
Stage-3 is filtered out by condition resolver.
Stage-5 is filtered out by condition resolver.
Moving data to directory hdfs://namenode:9000/data2/gasto/idtipogasto=3/.hive-staging_hive_2023-12-10_21-59-44_531_508544661930601567-1/-ext-10000
Loading data to table integrador2.gasto partition (idtipogasto=3)
MapReduce Jobs Launched:
Stage-Stage-1:  HDFS Read: 0 HDFS Write: 0 SUCCESS
Total MapReduce CPU Time Spent: 0 msec
OK
Time taken: 2.088 seconds
WARNING: Hive-on-MR is deprecated in Hive 2 and may not be available in the future versions. Consider using a different execution engine (i.e. spark, tez) or using Hive 1.X releases.
Query ID = root_20231210215946_47cec2d6-f26d-4937-aff0-d75c4c6b8b08
Total jobs = 3
Launching Job 1 out of 3
Number of reduce tasks is set to 0 since there's no reduce operator
Job running in-process (local Hadoop)
2023-12-10 21:59:49,405 Stage-1 map = 0%,  reduce = 0%
Ended Job = job_local444261840_0005
Stage-4 is selected by condition resolver.
Stage-3 is filtered out by condition resolver.
Stage-5 is filtered out by condition resolver.
Moving data to directory hdfs://namenode:9000/data2/gasto/idtipogasto=4/.hive-staging_hive_2023-12-10_21-59-46_633_1850635295236742414-1/-ext-10000
Loading data to table integrador2.gasto partition (idtipogasto=4)
MapReduce Jobs Launched:
Stage-Stage-1:  HDFS Read: 0 HDFS Write: 0 SUCCESS
Total MapReduce CPU Time Spent: 0 msec
OK
Time taken: 3.001 seconds
OK
Time taken: 0.053 seconds
OK
Time taken: 0.057 seconds
WARNING: Hive-on-MR is deprecated in Hive 2 and may not be available in the future versions. Consider using a different execution engine (i.e. spark, tez) or using Hive 1.X releases.
Query ID = root_20231210215949_9da3b7d0-1a0b-40d8-8e6d-f6303f0aefaa
Total jobs = 3
Launching Job 1 out of 3
Number of reduce tasks is set to 0 since there's no reduce operator
Job running in-process (local Hadoop)
2023-12-10 21:59:51,286 Stage-1 map = 0%,  reduce = 0%
Ended Job = job_local923498052_0006
Stage-4 is selected by condition resolver.
Stage-3 is filtered out by condition resolver.
Stage-5 is filtered out by condition resolver.
Moving data to directory hdfs://namenode:9000/data2/tipodegasto/.hive-staging_hive_2023-12-10_21-59-49_768_2699805631690417607-1/-ext-10000
Loading data to table integrador2.tipo_gasto
MapReduce Jobs Launched:
Stage-Stage-1:  HDFS Read: 0 HDFS Write: 0 SUCCESS
Total MapReduce CPU Time Spent: 0 msec
OK
Time taken: 2.215 seconds
OK
Time taken: 0.058 seconds
OK
Time taken: 0.045 seconds
WARNING: Hive-on-MR is deprecated in Hive 2 and may not be available in the future versions. Consider using a different execution engine (i.e. spark, tez) or using Hive 1.X releases.
Query ID = root_20231210215952_3d7ea03e-46b0-4a84-97b4-03366bf424b8
Total jobs = 3
Launching Job 1 out of 3
Number of reduce tasks is set to 0 since there's no reduce operator
Job running in-process (local Hadoop)
2023-12-10 21:59:54,466 Stage-1 map = 0%,  reduce = 0%
Ended Job = job_local1771815956_0007
Stage-4 is selected by condition resolver.
Stage-3 is filtered out by condition resolver.
Stage-5 is filtered out by condition resolver.
Moving data to directory hdfs://namenode:9000/data2/venta/.hive-staging_hive_2023-12-10_21-59-52_102_1484978777970684341-1/-ext-10000
Loading data to table integrador2.venta
MapReduce Jobs Launched:
Stage-Stage-1:  HDFS Read: 0 HDFS Write: 0 SUCCESS
Total MapReduce CPU Time Spent: 0 msec
OK
Time taken: 2.579 seconds
OK
Time taken: 0.042 seconds
OK
Time taken: 0.047 seconds
WARNING: Hive-on-MR is deprecated in Hive 2 and may not be available in the future versions. Consider using a different execution engine (i.e. spark, tez) or using Hive 1.X releases.
Query ID = root_20231210215954_cc7548af-0f5f-4027-bd76-950a750fb46f
Total jobs = 3
Launching Job 1 out of 3
Number of reduce tasks is set to 0 since there's no reduce operator
Job running in-process (local Hadoop)
2023-12-10 21:59:57,275 Stage-1 map = 0%,  reduce = 0%
Ended Job = job_local1805058919_0008
Stage-4 is selected by condition resolver.
Stage-3 is filtered out by condition resolver.
Stage-5 is filtered out by condition resolver.
Moving data to directory hdfs://namenode:9000/data2/canaldeventa/.hive-staging_hive_2023-12-10_21-59-54_786_2963561916846793907-1/-ext-10000
Loading data to table integrador2.canal_venta
MapReduce Jobs Launched:
Stage-Stage-1:  HDFS Read: 0 HDFS Write: 0 SUCCESS
Total MapReduce CPU Time Spent: 0 msec
OK
Time taken: 2.696 seconds
OK
Time taken: 0.049 seconds
OK
Time taken: 0.043 seconds
WARNING: Hive-on-MR is deprecated in Hive 2 and may not be available in the future versions. Consider using a different execution engine (i.e. spark, tez) or using Hive 1.X releases.
Query ID = root_20231210215957_22fc500a-9777-4b06-881d-f839191dde00
Total jobs = 3
Launching Job 1 out of 3
Number of reduce tasks is set to 0 since there's no reduce operator
Job running in-process (local Hadoop)
2023-12-10 21:59:59,005 Stage-1 map = 0%,  reduce = 0%
Ended Job = job_local63042021_0009
Stage-4 is selected by condition resolver.
Stage-3 is filtered out by condition resolver.
Stage-5 is filtered out by condition resolver.
Moving data to directory hdfs://namenode:9000/data2/cliente/.hive-staging_hive_2023-12-10_21-59-57_592_7288377494625053678-1/-ext-10000
Loading data to table integrador2.cliente
MapReduce Jobs Launched:
Stage-Stage-1:  HDFS Read: 0 HDFS Write: 0 SUCCESS
Total MapReduce CPU Time Spent: 0 msec
OK
Time taken: 1.825 seconds
OK
Time taken: 0.042 seconds
OK
Time taken: 0.05 seconds
WARNING: Hive-on-MR is deprecated in Hive 2 and may not be available in the future versions. Consider using a different execution engine (i.e. spark, tez) or using Hive 1.X releases.
Query ID = root_20231210215959_cd10e6cc-1f4f-4851-bf8f-7f8690f24d64
Total jobs = 3
Launching Job 1 out of 3
Number of reduce tasks is set to 0 since there's no reduce operator
Job running in-process (local Hadoop)
2023-12-10 22:00:02,096 Stage-1 map = 0%,  reduce = 0%
Ended Job = job_local482809270_0010
Stage-4 is selected by condition resolver.
Stage-3 is filtered out by condition resolver.
Stage-5 is filtered out by condition resolver.
Moving data to directory hdfs://namenode:9000/data2/producto/.hive-staging_hive_2023-12-10_21-59-59_528_4320547302185950896-1/-ext-10000
Loading data to table integrador2.producto
MapReduce Jobs Launched:
Stage-Stage-1:  HDFS Read: 0 HDFS Write: 0 SUCCESS
Total MapReduce CPU Time Spent: 0 msec
OK
Time taken: 3.1 seconds
OK
Time taken: 0.07 seconds
OK
Time taken: 0.042 seconds
WARNING: Hive-on-MR is deprecated in Hive 2 and may not be available in the future versions. Consider using a different execution engine (i.e. spark, tez) or using Hive 1.X releases.
Query ID = root_20231210220002_883198fc-e3d2-4bf5-86fa-aa222f59e65a
Total jobs = 3
Launching Job 1 out of 3
Number of reduce tasks is set to 0 since there's no reduce operator
Job running in-process (local Hadoop)
2023-12-10 22:00:06,574 Stage-1 map = 0%,  reduce = 0%
Ended Job = job_local1083941463_0011
Stage-4 is selected by condition resolver.
Stage-3 is filtered out by condition resolver.
Stage-5 is filtered out by condition resolver.
Moving data to directory hdfs://namenode:9000/data2/empleado/.hive-staging_hive_2023-12-10_22-00-02_792_8938999654882137433-1/-ext-10000
Loading data to table integrador2.empleado
MapReduce Jobs Launched:
Stage-Stage-1:  HDFS Read: 0 HDFS Write: 0 SUCCESS
Total MapReduce CPU Time Spent: 0 msec
OK
Time taken: 4.008 seconds
OK
Time taken: 0.044 seconds
OK
Time taken: 0.039 seconds
WARNING: Hive-on-MR is deprecated in Hive 2 and may not be available in the future versions. Consider using a different execution engine (i.e. spark, tez) or using Hive 1.X releases.
Query ID = root_20231210220006_13a4d716-477a-45ce-b77e-3e69de254380
Total jobs = 3
Launching Job 1 out of 3
Number of reduce tasks is set to 0 since there's no reduce operator
Job running in-process (local Hadoop)
2023-12-10 22:00:10,035 Stage-1 map = 0%,  reduce = 0%
Ended Job = job_local2088111129_0012
Stage-4 is selected by condition resolver.
Stage-3 is filtered out by condition resolver.
Stage-5 is filtered out by condition resolver.
Moving data to directory hdfs://namenode:9000/data2/sucursal/.hive-staging_hive_2023-12-10_22-00-06_898_1209306472789402596-1/-ext-10000
Loading data to table integrador2.sucursal
MapReduce Jobs Launched:
Stage-Stage-1:  HDFS Read: 0 HDFS Write: 0 SUCCESS
Total MapReduce CPU Time Spent: 0 msec
OK
Time taken: 3.357 seconds
OK
Time taken: 0.04 seconds
OK
Time taken: 0.086 seconds
WARNING: Hive-on-MR is deprecated in Hive 2 and may not be available in the future versions. Consider using a different execution engine (i.e. spark, tez) or using Hive 1.X releases.
Query ID = root_20231210220010_c75d233d-2794-477d-b7b6-0d1489831f8d
Total jobs = 3
Launching Job 1 out of 3
Number of reduce tasks is set to 0 since there's no reduce operator
Job running in-process (local Hadoop)
2023-12-10 22:00:12,971 Stage-1 map = 0%,  reduce = 0%
Ended Job = job_local1323814565_0013
Stage-4 is selected by condition resolver.
Stage-3 is filtered out by condition resolver.
Stage-5 is filtered out by condition resolver.
Moving data to directory hdfs://namenode:9000/data2/calendario/.hive-staging_hive_2023-12-10_22-00-10_399_7899942268310473109-1/-ext-10000
Loading data to table integrador2.calendario
MapReduce Jobs Launched:
Stage-Stage-1:  HDFS Read: 0 HDFS Write: 0 SUCCESS
Total MapReduce CPU Time Spent: 0 msec
OK
Time taken: 2.786 seconds
OK
Time taken: 0.045 seconds
OK
Time taken: 0.046 seconds
WARNING: Hive-on-MR is deprecated in Hive 2 and may not be available in the future versions. Consider using a different execution engine (i.e. spark, tez) or using Hive 1.X releases.
Query ID = root_20231210220013_692fb29c-86c9-4ab0-b3a3-c04fe8cb6c1b
Total jobs = 3
Launching Job 1 out of 3
Number of reduce tasks is set to 0 since there's no reduce operator
Job running in-process (local Hadoop)
2023-12-10 22:00:14,672 Stage-1 map = 0%,  reduce = 0%
Ended Job = job_local1764911307_0014
Stage-4 is selected by condition resolver.
Stage-3 is filtered out by condition resolver.
Stage-5 is filtered out by condition resolver.
Moving data to directory hdfs://namenode:9000/data2/proveedor/.hive-staging_hive_2023-12-10_22-00-13_290_4379775169629603082-1/-ext-10000
Loading data to table integrador2.proveedor
MapReduce Jobs Launched:
Stage-Stage-1:  HDFS Read: 0 HDFS Write: 0 SUCCESS
Total MapReduce CPU Time Spent: 0 msec
OK
Time taken: 1.608 seconds
root@67bd040ac32b:/opt# hive -f /home/Paso04.hql
SLF4J: Class path contains multiple SLF4J bindings.
SLF4J: Found binding in [jar:file:/opt/hive/lib/log4j-slf4j-impl-2.6.2.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: Found binding in [jar:file:/opt/hadoop-2.7.4/share/hadoop/common/lib/slf4j-log4j12-1.7.10.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: See http://www.slf4j.org/codes.html#multiple_bindings for an explanation.
SLF4J: Actual binding is of type [org.apache.logging.slf4j.Log4jLoggerFactory]

Logging initialized using configuration in file:/opt/hive/conf/hive-log4j2.properties Async: true
OK
Time taken: 4.102 seconds
OK
Time taken: 0.209 seconds
```
Luego de ejecutar los 3 archivo HQL revisamos que se encuentren en nuestro entorno


5) No-SQL

A) HBase:

Segun lo propuesto en el readme del proyecto realizamos la ejecucion del comando
```
adminstaller@Labo-AZ10:~/herramientas_big_data$ sudo docker exec -it hbase-master hbase shell
2023-12-10 22:06:39,898 WARN  [main] util.NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable
HBase Shell; enter 'help<RETURN>' for list of supported commands.
Type "exit<RETURN>" to leave the HBase Shell
Version 1.2.6, rUnknown, Mon May 29 02:25:32 CDT 2017
```
y ya en el shell script de hbase ejecutamos
```
  hbase(main):001:0> create 'personal','personal_data'
  hbase> create 't1', {NAME => 'f1'}, {NAME => 'f2'}, {NAME => 'f3'}
  hbase> # The above in shorthand would be the following:
  hbase> create 't1', 'f1', 'f2', 'f3'
  hbase> create 't1', {NAME => 'f1', VERSIONS => 1, TTL => 2592000, BLOCKCACHE => true}
  hbase> create 't1', {NAME => 'f1', CONFIGURATION => {'hbase.hstore.blockingStoreFiles' => '10'}}

Table configuration options can be put at the end.
Examples:

  hbase> create 'ns1:t1', 'f1', SPLITS => ['10', '20', '30', '40']
  hbase> create 't1', 'f1', SPLITS => ['10', '20', '30', '40']
  hbase> create 't1', 'f1', SPLITS_FILE => 'splits.txt', OWNER => 'johndoe'
  hbase> create 't1', {NAME => 'f1', VERSIONS => 5}, METADATA => { 'mykey' => 'myvalue' }
  hbase> # Optionally pre-split the table into NUMREGIONS, using
  hbase> # SPLITALGO ("HexStringSplit", "UniformSplit" or classname)
  hbase> create 't1', 'f1', {NUMREGIONS => 15, SPLITALGO => 'HexStringSplit'}
  hbase> create 't1', 'f1', {NUMREGIONS => 15, SPLITALGO => 'HexStringSplit', REGION_REPLICATION => 2, CONFIGURATION => {'hbase.hregion.scan.loadColumnFamiliesOnDemand' => 'true'}}
  hbase> create 't1', {NAME => 'f1', DFS_REPLICATION => 1}

You can also keep around a reference to the created table:

  hbase> t1 = create 't1', 'f1'

Which gives you a reference to the table named 't1', on which you can then
call methods.


hbase(main):002:0> list 'personal'
TABLE
personal
1 row(s) in 0.0200 seconds

=> ["personal"]
hbase(main):003:0> put 'personal',1,'personal_data:name','Juan'
0 row(s) in 0.2090 seconds

hbase(main):004:0> put 'personal',1,'personal_data:city','Córdoba'
0 row(s) in 0.0140 seconds

hbase(main):005:0> put 'personal',1,'personal_data:age','25'
0 row(s) in 0.0170 seconds

hbase(main):006:0> put 'personal',2,'personal_data:name','Franco'
0 row(s) in 0.0180 seconds

hbase(main):007:0> put 'personal',2,'personal_data:city','Lima'
0 row(s) in 0.0100 seconds

hbase(main):008:0> put 'personal',2,'personal_data:age','32'
0 row(s) in 0.0180 seconds

hbase(main):009:0> put 'personal',3,'personal_data:name','Ivan'
0 row(s) in 0.0110 seconds

hbase(main):010:0> put 'personal',3,'personal_data:age','34'
0 row(s) in 0.0100 seconds

hbase(main):011:0> put 'personal',4,'personal_data:name','Eliecer'
0 row(s) in 0.0450 seconds

hbase(main):012:0> put 'personal',4,'personal_data:city','Caracas'
0 row(s) in 0.0110 seconds

hbase(main):013:0> get 'personal','4'
COLUMN                                   CELL
 personal_data:city                      timestamp=1702246098371, value=Caracas
 personal_data:name                      timestamp=1702246092675, value=Eliecer
2 row(s) in 0.0480 seconds

hbase(main):014:0>
```
Luego de ejecutar estos scripts salimos del shell script de hbase con Ctrl+D y nos volvemos al cluster de namenode
```
hbase(main):014:0> adminstaller@Labo-AZ10:~/herramientas_big_data$ sudo docker exec -it namenode bash
```
y alli dentro ejecutamos
```
root@9b8bf947e163:/# hdfs dfs -put personal.csv /hbase/data/personal.csv
put: `/hbase/data/personal.csv': File exists
root@9b8bf947e163:/#
```
Luego nos movemos al shell de hbase.
```
adminstaller@Labo-AZ10:~/herramientas_big_data$ sudo docker exec -it hbase-master bash
root@hbase-master:/# hbase org.apache.hadoop.hbase.mapreduce.ImportTsv -Dimporttsv.separator=',' -Dimporttsv.columns=HBASE_ROW_KEY,personal_data:name,personal_data:city,personal_data:age personal hdfs://namenode:9000/hbase/data/personal.csv
2023-12-10 22:10:14,264 WARN  [main] util.NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable
2023-12-10 22:10:14,757 INFO  [main] zookeeper.RecoverableZooKeeper: Process identifier=hconnection-0x71a794e5 connecting to ZooKeeper ensemble=zoo:2181
2023-12-10 22:10:14,763 INFO  [main] zookeeper.ZooKeeper: Client environment:zookeeper.version=3.4.6-1569965, built on 02/20/2014 09:09 GMT
2023-12-10 22:10:14,763 INFO  [main] zookeeper.ZooKeeper: Client environment:host.name=hbase-master
2023-12-10 22:10:14,763 INFO  [main] zookeeper.ZooKeeper: Client environment:java.version=1.8.0_141
2023-12-10 22:10:14,763 INFO  [main] zookeeper.ZooKeeper: Client environment:java.vendor=Oracle Corporation
2023-12-10 22:10:14,763 INFO  [main] zookeeper.ZooKeeper: Client environment:java.home=/usr/lib/jvm/java-8-openjdk-amd64/jre
2023-12-10 22:10:14,764 INFO  [main] zookeeper.ZooKeeper: Client environment:java.class.path=/etc/hbase:/docker-java-home/lib/tools.jar:/opt/hbase-1.2.6/bin/..:/opt/hbase-1.2.6/bin/../lib/activation-1.1.jar:/opt/hbase-1.2.6/bin/../lib/aopalliance-1.0.jar:/opt/hbase-1.2.6/bin/../lib/apacheds-i18n-2.0.0-M15.jar:/opt/hbase-1.2.6/bin/../lib/apacheds-kerberos-codec-2.0.0-M15.jar:/opt/hbase-1.2.6/bin/../lib/api-asn1-api-1.0.0-M20.jar:/opt/hbase-1.2.6/bin/../lib/api-util-1.0.0-M20.jar:/opt/hbase-1.2.6/bin/../lib/asm-3.1.jar:/opt/hbase-1.2.6/bin/../lib/avro-1.7.4.jar:/opt/hbase-1.2.6/bin/../lib/commons-beanutils-1.7.0.jar:/opt/hbase-1.2.6/bin/../lib/commons-beanutils-core-1.8.0.jar:/opt/hbase-1.2.6/bin/../lib/commons-cli-1.2.jar:/opt/hbase-1.2.6/bin/../lib/commons-codec-1.9.jar:/opt/hbase-1.2.6/bin/../lib/commons-collections-3.2.2.jar:/opt/hbase-1.2.6/bin/../lib/commons-compress-1.4.1.jar:/opt/hbase-1.2.6/bin/../lib/commons-configuration-1.6.jar:/opt/hbase-1.2.6/bin/../lib/commons-daemon-1.0.13.jar:/opt/hbase-1.2.6/bin/../lib/commons-digester-1.8.jar:/opt/hbase-1.2.6/bin/../lib/commons-el-1.0.jar:/opt/hbase-1.2.6/bin/../lib/commons-httpclient-3.1.jar:/opt/hbase-1.2.6/bin/../lib/commons-io-2.4.jar:/opt/hbase-1.2.6/bin/../lib/commons-lang-2.6.jar:/opt/hbase-1.2.6/bin/../lib/commons-logging-1.2.jar:/opt/hbase-1.2.6/bin/../lib/commons-math-2.2.jar:/opt/hbase-1.2.6/bin/../lib/commons-math3-3.1.1.jar:/opt/hbase-1.2.6/bin/../lib/commons-net-3.1.jar:/opt/hbase-1.2.6/bin/../lib/disruptor-3.3.0.jar:/opt/hbase-1.2.6/bin/../lib/findbugs-annotations-1.3.9-1.jar:/opt/hbase-1.2.6/bin/../lib/guava-12.0.1.jar:/opt/hbase-1.2.6/bin/../lib/guice-3.0.jar:/opt/hbase-1.2.6/bin/../lib/guice-servlet-3.0.jar:/opt/hbase-1.2.6/bin/../lib/hadoop-annotations-2.5.1.jar:/opt/hbase-1.2.6/bin/../lib/hadoop-auth-2.5.1.jar:/opt/hbase-1.2.6/bin/../lib/hadoop-client-2.5.1.jar:/opt/hbase-1.2.6/bin/../lib/hadoop-common-2.5.1.jar:/opt/hbase-1.2.6/bin/../lib/hadoop-hdfs-2.5.1.jar:/opt/hbase-1.2.6/bin/../lib/hadoop-mapreduce-client-app-2.5.1.jar:/opt/hbase-1.2.6/bin/../lib/hadoop-mapreduce-client-common-2.5.1.jar:/opt/hbase-1.2.6/bin/../lib/hadoop-mapreduce-client-core-2.5.1.jar:/opt/hbase-1.2.6/bin/../lib/hadoop-mapreduce-client-jobclient-2.5.1.jar:/opt/hbase-1.2.6/bin/../lib/hadoop-mapreduce-client-shuffle-2.5.1.jar:/opt/hbase-1.2.6/bin/../lib/hadoop-yarn-api-2.5.1.jar:/opt/hbase-1.2.6/bin/../lib/hadoop-yarn-client-2.5.1.jar:/opt/hbase-1.2.6/bin/../lib/hadoop-yarn-common-2.5.1.jar:/opt/hbase-1.2.6/bin/../lib/hadoop-yarn-server-common-2.5.1.jar:/opt/hbase-1.2.6/bin/../lib/hbase-annotations-1.2.6-tests.jar:/opt/hbase-1.2.6/bin/../lib/hbase-annotations-1.2.6.jar:/opt/hbase-1.2.6/bin/../lib/hbase-client-1.2.6.jar:/opt/hbase-1.2.6/bin/../lib/hbase-common-1.2.6-tests.jar:/opt/hbase-1.2.6/bin/../lib/hbase-common-1.2.6.jar:/opt/hbase-1.2.6/bin/../lib/hbase-examples-1.2.6.jar:/opt/hbase-1.2.6/bin/../lib/hbase-external-blockcache-1.2.6.jar:/opt/hbase-1.2.6/bin/../lib/hbase-hadoop-compat-1.2.6.jar:/opt/hbase-1.2.6/bin/../lib/hbase-hadoop2-compat-1.2.6.jar:/opt/hbase-1.2.6/bin/../lib/hbase-it-1.2.6-tests.jar:/opt/hbase-1.2.6/bin/../lib/hbase-it-1.2.6.jar:/opt/hbase-1.2.6/bin/../lib/hbase-prefix-tree-1.2.6.jar:/opt/hbase-1.2.6/bin/../lib/hbase-procedure-1.2.6.jar:/opt/hbase-1.2.6/bin/../lib/hbase-protocol-1.2.6.jar:/opt/hbase-1.2.6/bin/../lib/hbase-resource-bundle-1.2.6.jar:/opt/hbase-1.2.6/bin/../lib/hbase-rest-1.2.6.jar:/opt/hbase-1.2.6/bin/../lib/hbase-server-1.2.6-tests.jar:/opt/hbase-1.2.6/bin/../lib/hbase-server-1.2.6.jar:/opt/hbase-1.2.6/bin/../lib/hbase-shell-1.2.6.jar:/opt/hbase-1.2.6/bin/../lib/hbase-thrift-1.2.6.jar:/opt/hbase-1.2.6/bin/../lib/htrace-core-3.1.0-incubating.jar:/opt/hbase-1.2.6/bin/../lib/httpclient-4.2.5.jar:/opt/hbase-1.2.6/bin/../lib/httpcore-4.4.1.jar:/opt/hbase-1.2.6/bin/../lib/jackson-core-asl-1.9.13.jar:/opt/hbase-1.2.6/bin/../lib/jackson-jaxrs-1.9.13.jar:/opt/hbase-1.2.6/bin/../lib/jackson-mapper-asl-1.9.13.jar:/opt/hbase-1.2.6/bin/../lib/jackson-xc-1.9.13.jar:/opt/hbase-1.2.6/bin/../lib/jamon-runtime-2.4.1.jar:/opt/hbase-1.2.6/bin/../lib/jasper-compiler-5.5.23.jar:/opt/hbase-1.2.6/bin/../lib/jasper-runtime-5.5.23.jar:/opt/hbase-1.2.6/bin/../lib/java-xmlbuilder-0.4.jar:/opt/hbase-1.2.6/bin/../lib/javax.inject-1.jar:/opt/hbase-1.2.6/bin/../lib/jaxb-api-2.2.2.jar:/opt/hbase-1.2.6/bin/../lib/jaxb-impl-2.2.3-1.jar:/opt/hbase-1.2.6/bin/../lib/jcodings-1.0.8.jar:/opt/hbase-1.2.6/bin/../lib/jersey-client-1.9.jar:/opt/hbase-1.2.6/bin/../lib/jersey-core-1.9.jar:/opt/hbase-1.2.6/bin/../lib/jersey-guice-1.9.jar:/opt/hbase-1.2.6/bin/../lib/jersey-json-1.9.jar:/opt/hbase-1.2.6/bin/../lib/jersey-server-1.9.jar:/opt/hbase-1.2.6/bin/../lib/jets3t-0.9.0.jar:/opt/hbase-1.2.6/bin/../lib/jettison-1.3.3.jar:/opt/hbase-1.2.6/bin/../lib/jetty-6.1.26.jar:/opt/hbase-1.2.6/bin/../lib/jetty-sslengine-6.1.26.jar:/opt/hbase-1.2.6/bin/../lib/jetty-util-6.1.26.jar:/opt/hbase-1.2.6/bin/../lib/joni-2.1.2.jar:/opt/hbase-1.2.6/bin/../lib/jruby-complete-1.6.8.jar:/opt/hbase-1.2.6/bin/../lib/jsch-0.1.42.jar:/opt/hbase-1.2.6/bin/../lib/jsp-2.1-6.1.14.jar:/opt/hbase-1.2.6/bin/../lib/jsp-api-2.1-6.1.14.jar:/opt/hbase-1.2.6/bin/../lib/junit-4.12.jar:/opt/hbase-1.2.6/bin/../lib/leveldbjni-all-1.8.jar:/opt/hbase-1.2.6/bin/../lib/libthrift-0.9.3.jar:/opt/hbase-1.2.6/bin/../lib/log4j-1.2.17.jar:/opt/hbase-1.2.6/bin/../lib/metrics-core-2.2.0.jar:/opt/hbase-1.2.6/bin/../lib/netty-all-4.0.23.Final.jar:/opt/hbase-1.2.6/bin/../lib/paranamer-2.3.jar:/opt/hbase-1.2.6/bin/../lib/protobuf-java-2.5.0.jar:/opt/hbase-1.2.6/bin/../lib/servlet-api-2.5-6.1.14.jar:/opt/hbase-1.2.6/bin/../lib/servlet-api-2.5.jar:/opt/hbase-1.2.6/bin/../lib/slf4j-api-1.7.7.jar:/opt/hbase-1.2.6/bin/../lib/slf4j-log4j12-1.7.5.jar:/opt/hbase-1.2.6/bin/../lib/snappy-java-1.0.4.1.jar:/opt/hbase-1.2.6/bin/../lib/spymemcached-2.11.6.jar:/opt/hbase-1.2.6/bin/../lib/xmlenc-0.52.jar:/opt/hbase-1.2.6/bin/../lib/xz-1.0.jar:/opt/hbase-1.2.6/bin/../lib/zookeeper-3.4.6.jar:
2023-12-10 22:10:14,764 INFO  [main] zookeeper.ZooKeeper: Client environment:java.library.path=/usr/java/packages/lib/amd64:/usr/lib/x86_64-linux-gnu/jni:/lib/x86_64-linux-gnu:/usr/lib/x86_64-linux-gnu:/usr/lib/jni:/lib:/usr/lib
2023-12-10 22:10:14,764 INFO  [main] zookeeper.ZooKeeper: Client environment:java.io.tmpdir=/tmp
2023-12-10 22:10:14,764 INFO  [main] zookeeper.ZooKeeper: Client environment:java.compiler=<NA>
2023-12-10 22:10:14,765 INFO  [main] zookeeper.ZooKeeper: Client environment:os.name=Linux
2023-12-10 22:10:14,765 INFO  [main] zookeeper.ZooKeeper: Client environment:os.arch=amd64
2023-12-10 22:10:14,765 INFO  [main] zookeeper.ZooKeeper: Client environment:os.version=5.15.0-1052-azure
2023-12-10 22:10:14,765 INFO  [main] zookeeper.ZooKeeper: Client environment:user.name=root
2023-12-10 22:10:14,765 INFO  [main] zookeeper.ZooKeeper: Client environment:user.home=/root
2023-12-10 22:10:14,766 INFO  [main] zookeeper.ZooKeeper: Client environment:user.dir=/
2023-12-10 22:10:14,766 INFO  [main] zookeeper.ZooKeeper: Initiating client connection, connectString=zoo:2181 sessionTimeout=90000 watcher=hconnection-0x71a794e50x0, quorum=zoo:2181, baseZNode=/hbase
2023-12-10 22:10:14,796 INFO  [main-SendThread(zoo.herramientas_big_data_default:2181)] zookeeper.ClientCnxn: Opening socket connection to server zoo.herramientas_big_data_default/172.19.0.13:2181. Will not attempt to authenticate using SASL (unknown error)
2023-12-10 22:10:14,808 INFO  [main-SendThread(zoo.herramientas_big_data_default:2181)] zookeeper.ClientCnxn: Socket connection established to zoo.herramientas_big_data_default/172.19.0.13:2181, initiating session
2023-12-10 22:10:15,195 INFO  [main-SendThread(zoo.herramientas_big_data_default:2181)] zookeeper.ClientCnxn: Session establishment complete on server zoo.herramientas_big_data_default/172.19.0.13:2181, sessionid = 0x18c55bb6af90004, negotiated timeout = 40000
2023-12-10 22:10:17,091 INFO  [main] Configuration.deprecation: io.bytes.per.checksum is deprecated. Instead, use dfs.bytes-per-checksum
2023-12-10 22:10:17,130 INFO  [main] client.ConnectionManager$HConnectionImplementation: Closing zookeeper sessionid=0x18c55bb6af90004
2023-12-10 22:10:17,140 INFO  [main] zookeeper.ZooKeeper: Session: 0x18c55bb6af90004 closed
2023-12-10 22:10:17,140 INFO  [main-EventThread] zookeeper.ClientCnxn: EventThread shut down
2023-12-10 22:10:17,184 INFO  [main] Configuration.deprecation: session.id is deprecated. Instead, use dfs.metrics.session-id
2023-12-10 22:10:17,185 INFO  [main] jvm.JvmMetrics: Initializing JVM Metrics with processName=JobTracker, sessionId=
2023-12-10 22:10:17,208 INFO  [main] Configuration.deprecation: io.bytes.per.checksum is deprecated. Instead, use dfs.bytes-per-checksum
2023-12-10 22:10:17,599 INFO  [main] input.FileInputFormat: Total input paths to process : 1
2023-12-10 22:10:17,678 INFO  [main] mapreduce.JobSubmitter: number of splits:1
2023-12-10 22:10:17,808 INFO  [main] mapreduce.JobSubmitter: Submitting tokens for job: job_local91503944_0001
2023-12-10 22:10:17,845 WARN  [main] conf.Configuration: file:/tmp/hadoop-root/mapred/staging/root91503944/.staging/job_local91503944_0001/job.xml:an attempt to override final parameter: mapreduce.job.end-notification.max.retry.interval;  Ignoring.
2023-12-10 22:10:17,848 WARN  [main] conf.Configuration: file:/tmp/hadoop-root/mapred/staging/root91503944/.staging/job_local91503944_0001/job.xml:an attempt to override final parameter: mapreduce.job.end-notification.max.attempts;  Ignoring.
2023-12-10 22:10:18,545 INFO  [main] mapred.LocalDistributedCacheManager: Creating symlink: /tmp/hadoop-root/mapred/local/1702246217898/hbase-server-1.2.6.jar <- //hbase-server-1.2.6.jar
2023-12-10 22:10:18,550 INFO  [main] mapred.LocalDistributedCacheManager: Localized file:/opt/hbase-1.2.6/lib/hbase-server-1.2.6.jar as file:/tmp/hadoop-root/mapred/local/1702246217898/hbase-server-1.2.6.jar
2023-12-10 22:10:18,550 INFO  [main] mapred.LocalDistributedCacheManager: Creating symlink: /tmp/hadoop-root/mapred/local/1702246217899/hbase-client-1.2.6.jar <- //hbase-client-1.2.6.jar
2023-12-10 22:10:18,553 INFO  [main] mapred.LocalDistributedCacheManager: Localized file:/opt/hbase-1.2.6/lib/hbase-client-1.2.6.jar as file:/tmp/hadoop-root/mapred/local/1702246217899/hbase-client-1.2.6.jar
2023-12-10 22:10:18,553 INFO  [main] mapred.LocalDistributedCacheManager: Creating symlink: /tmp/hadoop-root/mapred/local/1702246217900/zookeeper-3.4.6.jar <- //zookeeper-3.4.6.jar
2023-12-10 22:10:18,555 INFO  [main] mapred.LocalDistributedCacheManager: Localized file:/opt/hbase-1.2.6/lib/zookeeper-3.4.6.jar as file:/tmp/hadoop-root/mapred/local/1702246217900/zookeeper-3.4.6.jar
2023-12-10 22:10:18,555 INFO  [main] mapred.LocalDistributedCacheManager: Creating symlink: /tmp/hadoop-root/mapred/local/1702246217901/metrics-core-2.2.0.jar <- //metrics-core-2.2.0.jar
2023-12-10 22:10:18,557 INFO  [main] mapred.LocalDistributedCacheManager: Localized file:/opt/hbase-1.2.6/lib/metrics-core-2.2.0.jar as file:/tmp/hadoop-root/mapred/local/1702246217901/metrics-core-2.2.0.jar
2023-12-10 22:10:18,557 INFO  [main] mapred.LocalDistributedCacheManager: Creating symlink: /tmp/hadoop-root/mapred/local/1702246217902/protobuf-java-2.5.0.jar <- //protobuf-java-2.5.0.jar
2023-12-10 22:10:18,562 INFO  [main] mapred.LocalDistributedCacheManager: Localized file:/opt/hbase-1.2.6/lib/protobuf-java-2.5.0.jar as file:/tmp/hadoop-root/mapred/local/1702246217902/protobuf-java-2.5.0.jar
2023-12-10 22:10:18,562 INFO  [main] mapred.LocalDistributedCacheManager: Creating symlink: /tmp/hadoop-root/mapred/local/1702246217903/hadoop-mapreduce-client-core-2.5.1.jar <- //hadoop-mapreduce-client-core-2.5.1.jar
2023-12-10 22:10:18,564 INFO  [main] mapred.LocalDistributedCacheManager: Localized file:/opt/hbase-1.2.6/lib/hadoop-mapreduce-client-core-2.5.1.jar as file:/tmp/hadoop-root/mapred/local/1702246217903/hadoop-mapreduce-client-core-2.5.1.jar
2023-12-10 22:10:18,565 INFO  [main] mapred.LocalDistributedCacheManager: Creating symlink: /tmp/hadoop-root/mapred/local/1702246217904/hbase-common-1.2.6.jar <- //hbase-common-1.2.6.jar
2023-12-10 22:10:18,570 INFO  [main] mapred.LocalDistributedCacheManager: Localized file:/opt/hbase-1.2.6/lib/hbase-common-1.2.6.jar as file:/tmp/hadoop-root/mapred/local/1702246217904/hbase-common-1.2.6.jar
2023-12-10 22:10:18,570 INFO  [main] mapred.LocalDistributedCacheManager: Creating symlink: /tmp/hadoop-root/mapred/local/1702246217905/hbase-prefix-tree-1.2.6.jar <- //hbase-prefix-tree-1.2.6.jar
2023-12-10 22:10:18,572 INFO  [main] mapred.LocalDistributedCacheManager: Localized file:/opt/hbase-1.2.6/lib/hbase-prefix-tree-1.2.6.jar as file:/tmp/hadoop-root/mapred/local/1702246217905/hbase-prefix-tree-1.2.6.jar
2023-12-10 22:10:18,572 INFO  [main] mapred.LocalDistributedCacheManager: Creating symlink: /tmp/hadoop-root/mapred/local/1702246217906/htrace-core-3.1.0-incubating.jar <- //htrace-core-3.1.0-incubating.jar
2023-12-10 22:10:18,575 INFO  [main] mapred.LocalDistributedCacheManager: Localized file:/opt/hbase-1.2.6/lib/htrace-core-3.1.0-incubating.jar as file:/tmp/hadoop-root/mapred/local/1702246217906/htrace-core-3.1.0-incubating.jar
2023-12-10 22:10:18,575 INFO  [main] mapred.LocalDistributedCacheManager: Creating symlink: /tmp/hadoop-root/mapred/local/1702246217907/hadoop-common-2.5.1.jar <- //hadoop-common-2.5.1.jar
2023-12-10 22:10:18,579 INFO  [main] mapred.LocalDistributedCacheManager: Localized file:/opt/hbase-1.2.6/lib/hadoop-common-2.5.1.jar as file:/tmp/hadoop-root/mapred/local/1702246217907/hadoop-common-2.5.1.jar
2023-12-10 22:10:18,579 INFO  [main] mapred.LocalDistributedCacheManager: Creating symlink: /tmp/hadoop-root/mapred/local/1702246217908/hbase-protocol-1.2.6.jar <- //hbase-protocol-1.2.6.jar
2023-12-10 22:10:18,583 INFO  [main] mapred.LocalDistributedCacheManager: Localized file:/opt/hbase-1.2.6/lib/hbase-protocol-1.2.6.jar as file:/tmp/hadoop-root/mapred/local/1702246217908/hbase-protocol-1.2.6.jar
2023-12-10 22:10:18,583 INFO  [main] mapred.LocalDistributedCacheManager: Creating symlink: /tmp/hadoop-root/mapred/local/1702246217909/guava-12.0.1.jar <- //guava-12.0.1.jar
2023-12-10 22:10:18,586 INFO  [main] mapred.LocalDistributedCacheManager: Localized file:/opt/hbase-1.2.6/lib/guava-12.0.1.jar as file:/tmp/hadoop-root/mapred/local/1702246217909/guava-12.0.1.jar
2023-12-10 22:10:18,586 INFO  [main] mapred.LocalDistributedCacheManager: Creating symlink: /tmp/hadoop-root/mapred/local/1702246217910/hbase-hadoop-compat-1.2.6.jar <- //hbase-hadoop-compat-1.2.6.jar
2023-12-10 22:10:18,590 INFO  [main] mapred.LocalDistributedCacheManager: Localized file:/opt/hbase-1.2.6/lib/hbase-hadoop-compat-1.2.6.jar as file:/tmp/hadoop-root/mapred/local/1702246217910/hbase-hadoop-compat-1.2.6.jar
2023-12-10 22:10:18,592 INFO  [main] mapred.LocalDistributedCacheManager: Creating symlink: /tmp/hadoop-root/mapred/local/1702246217911/netty-all-4.0.23.Final.jar <- //netty-all-4.0.23.Final.jar
2023-12-10 22:10:18,594 INFO  [main] mapred.LocalDistributedCacheManager: Localized file:/opt/hbase-1.2.6/lib/netty-all-4.0.23.Final.jar as file:/tmp/hadoop-root/mapred/local/1702246217911/netty-all-4.0.23.Final.jar
2023-12-10 22:10:18,621 WARN  [main] conf.Configuration: file:/tmp/hadoop-root/mapred/local/localRunner/root/job_local91503944_0001/job_local91503944_0001.xml:an attempt to override final parameter: mapreduce.job.end-notification.max.retry.interval;  Ignoring.
2023-12-10 22:10:18,623 WARN  [main] conf.Configuration: file:/tmp/hadoop-root/mapred/local/localRunner/root/job_local91503944_0001/job_local91503944_0001.xml:an attempt to override final parameter: mapreduce.job.end-notification.max.attempts;  Ignoring.
2023-12-10 22:10:18,624 INFO  [main] mapred.LocalDistributedCacheManager: file:/tmp/hadoop-root/mapred/local/1702246217898/hbase-server-1.2.6.jar
2023-12-10 22:10:18,624 INFO  [main] mapred.LocalDistributedCacheManager: file:/tmp/hadoop-root/mapred/local/1702246217899/hbase-client-1.2.6.jar
2023-12-10 22:10:18,624 INFO  [main] mapred.LocalDistributedCacheManager: file:/tmp/hadoop-root/mapred/local/1702246217900/zookeeper-3.4.6.jar
2023-12-10 22:10:18,625 INFO  [main] mapred.LocalDistributedCacheManager: file:/tmp/hadoop-root/mapred/local/1702246217901/metrics-core-2.2.0.jar
2023-12-10 22:10:18,625 INFO  [main] mapred.LocalDistributedCacheManager: file:/tmp/hadoop-root/mapred/local/1702246217902/protobuf-java-2.5.0.jar
2023-12-10 22:10:18,626 INFO  [main] mapred.LocalDistributedCacheManager: file:/tmp/hadoop-root/mapred/local/1702246217903/hadoop-mapreduce-client-core-2.5.1.jar
2023-12-10 22:10:18,626 INFO  [main] mapred.LocalDistributedCacheManager: file:/tmp/hadoop-root/mapred/local/1702246217904/hbase-common-1.2.6.jar
2023-12-10 22:10:18,626 INFO  [main] mapred.LocalDistributedCacheManager: file:/tmp/hadoop-root/mapred/local/1702246217905/hbase-prefix-tree-1.2.6.jar
2023-12-10 22:10:18,627 INFO  [main] mapred.LocalDistributedCacheManager: file:/tmp/hadoop-root/mapred/local/1702246217906/htrace-core-3.1.0-incubating.jar
2023-12-10 22:10:18,627 INFO  [main] mapred.LocalDistributedCacheManager: file:/tmp/hadoop-root/mapred/local/1702246217907/hadoop-common-2.5.1.jar
2023-12-10 22:10:18,627 INFO  [main] mapred.LocalDistributedCacheManager: file:/tmp/hadoop-root/mapred/local/1702246217908/hbase-protocol-1.2.6.jar
2023-12-10 22:10:18,628 INFO  [main] mapred.LocalDistributedCacheManager: file:/tmp/hadoop-root/mapred/local/1702246217909/guava-12.0.1.jar
2023-12-10 22:10:18,628 INFO  [main] mapred.LocalDistributedCacheManager: file:/tmp/hadoop-root/mapred/local/1702246217910/hbase-hadoop-compat-1.2.6.jar
2023-12-10 22:10:18,628 INFO  [main] mapred.LocalDistributedCacheManager: file:/tmp/hadoop-root/mapred/local/1702246217911/netty-all-4.0.23.Final.jar
2023-12-10 22:10:18,637 INFO  [main] mapreduce.Job: The url to track the job: http://localhost:8080/
2023-12-10 22:10:18,638 INFO  [main] mapreduce.Job: Running job: job_local91503944_0001
2023-12-10 22:10:18,640 INFO  [Thread-34] mapred.LocalJobRunner: OutputCommitter set in config null
2023-12-10 22:10:18,662 INFO  [Thread-34] Configuration.deprecation: io.bytes.per.checksum is deprecated. Instead, use dfs.bytes-per-checksum
2023-12-10 22:10:18,664 INFO  [Thread-34] mapred.LocalJobRunner: OutputCommitter is org.apache.hadoop.hbase.mapreduce.TableOutputCommitter
2023-12-10 22:10:18,685 INFO  [Thread-34] mapred.LocalJobRunner: Waiting for map tasks
2023-12-10 22:10:18,687 INFO  [LocalJobRunner Map Task Executor #0] mapred.LocalJobRunner: Starting task: attempt_local91503944_0001_m_000000_0
2023-12-10 22:10:18,739 INFO  [LocalJobRunner Map Task Executor #0] mapred.Task:  Using ResourceCalculatorProcessTree : [ ]
2023-12-10 22:10:18,743 INFO  [LocalJobRunner Map Task Executor #0] mapred.MapTask: Processing split: hdfs://namenode:9000/hbase/data/personal.csv:0+94
2023-12-10 22:10:18,751 INFO  [LocalJobRunner Map Task Executor #0] zookeeper.RecoverableZooKeeper: Process identifier=hconnection-0x3fc97f55 connecting to ZooKeeper ensemble=zoo:2181
2023-12-10 22:10:18,751 INFO  [LocalJobRunner Map Task Executor #0] zookeeper.ZooKeeper: Initiating client connection, connectString=zoo:2181 sessionTimeout=90000 watcher=hconnection-0x3fc97f550x0, quorum=zoo:2181, baseZNode=/hbase
2023-12-10 22:10:18,757 INFO  [LocalJobRunner Map Task Executor #0-SendThread(zoo.herramientas_big_data_default:2181)] zookeeper.ClientCnxn: Opening socket connection to server zoo.herramientas_big_data_default/172.19.0.13:2181. Will not attempt to authenticate using SASL (unknown error)
2023-12-10 22:10:18,759 INFO  [LocalJobRunner Map Task Executor #0-SendThread(zoo.herramientas_big_data_default:2181)] zookeeper.ClientCnxn: Socket connection established to zoo.herramientas_big_data_default/172.19.0.13:2181, initiating session
2023-12-10 22:10:18,768 INFO  [LocalJobRunner Map Task Executor #0-SendThread(zoo.herramientas_big_data_default:2181)] zookeeper.ClientCnxn: Session establishment complete on server zoo.herramientas_big_data_default/172.19.0.13:2181, sessionid = 0x18c55bb6af90005, negotiated timeout = 40000
2023-12-10 22:10:18,773 INFO  [LocalJobRunner Map Task Executor #0] mapreduce.TableOutputFormat: Created table instance for personal
2023-12-10 22:10:18,797 INFO  [LocalJobRunner Map Task Executor #0] zookeeper.RecoverableZooKeeper: Process identifier=hconnection-0x5b3fa7cc connecting to ZooKeeper ensemble=zoo:2181
2023-12-10 22:10:18,797 INFO  [LocalJobRunner Map Task Executor #0] zookeeper.ZooKeeper: Initiating client connection, connectString=zoo:2181 sessionTimeout=90000 watcher=hconnection-0x5b3fa7cc0x0, quorum=zoo:2181, baseZNode=/hbase
2023-12-10 22:10:18,805 INFO  [LocalJobRunner Map Task Executor #0-SendThread(zoo.herramientas_big_data_default:2181)] zookeeper.ClientCnxn: Opening socket connection to server zoo.herramientas_big_data_default/172.19.0.13:2181. Will not attempt to authenticate using SASL (unknown error)
2023-12-10 22:10:18,806 INFO  [LocalJobRunner Map Task Executor #0-SendThread(zoo.herramientas_big_data_default:2181)] zookeeper.ClientCnxn: Socket connection established to zoo.herramientas_big_data_default/172.19.0.13:2181, initiating session
2023-12-10 22:10:18,817 INFO  [LocalJobRunner Map Task Executor #0-SendThread(zoo.herramientas_big_data_default:2181)] zookeeper.ClientCnxn: Session establishment complete on server zoo.herramientas_big_data_default/172.19.0.13:2181, sessionid = 0x18c55bb6af90006, negotiated timeout = 40000
2023-12-10 22:10:18,847 ERROR [LocalJobRunner Map Task Executor #0] mapreduce.DefaultVisibilityExpressionResolver: Error scanning 'labels' table
org.apache.hadoop.hbase.TableNotFoundException: Table 'hbase:labels' was not found, got: album.
        at org.apache.hadoop.hbase.client.ConnectionManager$HConnectionImplementation.locateRegionInMeta(ConnectionManager.java:1300)
        at org.apache.hadoop.hbase.client.ConnectionManager$HConnectionImplementation.locateRegion(ConnectionManager.java:1181)
        at org.apache.hadoop.hbase.client.RpcRetryingCallerWithReadReplicas.getRegionLocations(RpcRetryingCallerWithReadReplicas.java:305)
        at org.apache.hadoop.hbase.client.ScannerCallableWithReplicas.call(ScannerCallableWithReplicas.java:156)
        at org.apache.hadoop.hbase.client.ScannerCallableWithReplicas.call(ScannerCallableWithReplicas.java:60)
        at org.apache.hadoop.hbase.client.RpcRetryingCaller.callWithoutRetries(RpcRetryingCaller.java:210)
        at org.apache.hadoop.hbase.client.ClientScanner.call(ClientScanner.java:327)
        at org.apache.hadoop.hbase.client.ClientScanner.nextScanner(ClientScanner.java:302)
        at org.apache.hadoop.hbase.client.ClientScanner.initializeScannerInConstruction(ClientScanner.java:167)
        at org.apache.hadoop.hbase.client.ClientScanner.<init>(ClientScanner.java:162)
        at org.apache.hadoop.hbase.client.HTable.getScanner(HTable.java:797)
        at org.apache.hadoop.hbase.mapreduce.DefaultVisibilityExpressionResolver.init(DefaultVisibilityExpressionResolver.java:91)
        at org.apache.hadoop.hbase.mapreduce.CellCreator.<init>(CellCreator.java:48)
        at org.apache.hadoop.hbase.mapreduce.TsvImporterMapper.setup(TsvImporterMapper.java:108)
        at org.apache.hadoop.mapreduce.Mapper.run(Mapper.java:142)
        at org.apache.hadoop.mapred.MapTask.runNewMapper(MapTask.java:764)
        at org.apache.hadoop.mapred.MapTask.run(MapTask.java:340)
        at org.apache.hadoop.mapred.LocalJobRunner$Job$MapTaskRunnable.run(LocalJobRunner.java:243)
        at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:511)
        at java.util.concurrent.FutureTask.run(FutureTask.java:266)
        at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1149)
        at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:624)
        at java.lang.Thread.run(Thread.java:748)
2023-12-10 22:10:18,860 INFO  [LocalJobRunner Map Task Executor #0] client.ConnectionManager$HConnectionImplementation: Closing zookeeper sessionid=0x18c55bb6af90006
2023-12-10 22:10:18,867 INFO  [LocalJobRunner Map Task Executor #0] zookeeper.ZooKeeper: Session: 0x18c55bb6af90006 closed
2023-12-10 22:10:18,867 INFO  [LocalJobRunner Map Task Executor #0-EventThread] zookeeper.ClientCnxn: EventThread shut down
2023-12-10 22:10:18,939 INFO  [LocalJobRunner Map Task Executor #0] mapred.LocalJobRunner:
2023-12-10 22:10:19,013 INFO  [LocalJobRunner Map Task Executor #0] client.ConnectionManager$HConnectionImplementation: Closing zookeeper sessionid=0x18c55bb6af90005
2023-12-10 22:10:19,019 INFO  [LocalJobRunner Map Task Executor #0] zookeeper.ZooKeeper: Session: 0x18c55bb6af90005 closed
2023-12-10 22:10:19,019 INFO  [LocalJobRunner Map Task Executor #0-EventThread] zookeeper.ClientCnxn: EventThread shut down
2023-12-10 22:10:19,030 INFO  [LocalJobRunner Map Task Executor #0] mapred.Task: Task:attempt_local91503944_0001_m_000000_0 is done. And is in the process of committing
2023-12-10 22:10:19,037 INFO  [LocalJobRunner Map Task Executor #0] mapred.LocalJobRunner: map
2023-12-10 22:10:19,037 INFO  [LocalJobRunner Map Task Executor #0] mapred.Task: Task 'attempt_local91503944_0001_m_000000_0' done.
2023-12-10 22:10:19,037 INFO  [LocalJobRunner Map Task Executor #0] mapred.LocalJobRunner: Finishing task: attempt_local91503944_0001_m_000000_0
2023-12-10 22:10:19,038 INFO  [Thread-34] mapred.LocalJobRunner: map task executor complete.
2023-12-10 22:10:19,641 INFO  [main] mapreduce.Job: Job job_local91503944_0001 running in uber mode : false
2023-12-10 22:10:19,642 INFO  [main] mapreduce.Job:  map 100% reduce 0%
2023-12-10 22:10:19,644 INFO  [main] mapreduce.Job: Job job_local91503944_0001 completed successfully
2023-12-10 22:10:19,662 INFO  [main] mapreduce.Job: Counters: 24
        File System Counters
                FILE: Number of bytes read=25671041
                FILE: Number of bytes written=26163860
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=94
                HDFS: Number of bytes written=0
                HDFS: Number of read operations=3
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=0
        Map-Reduce Framework
                Map input records=4
                Map output records=4
                Input split bytes=109
                Spilled Records=0
                Failed Shuffles=0
                Merged Map outputs=0
                GC time elapsed (ms)=0
                CPU time spent (ms)=0
                Physical memory (bytes) snapshot=0
                Virtual memory (bytes) snapshot=0
                Total committed heap usage (bytes)=125698048
        ImportTsv
                Bad Lines=0
        File Input Format Counters
                Bytes Read=94
        File Output Format Counters
                Bytes Written=0
```
y ya dentro del shell ejecutamos 

```
root@hbase-master:/# hbase shell
2023-12-10 22:10:41,580 WARN  [main] util.NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable
HBase Shell; enter 'help<RETURN>' for list of supported commands.
Type "exit<RETURN>" to leave the HBase Shell
Version 1.2.6, rUnknown, Mon May 29 02:25:32 CDT 2017
hbase(main):001:0> scan 'personal'
ROW                                      COLUMN+CELL
 1                                       column=personal_data:age, timestamp=1702246037598, value=25
 1                                       column=personal_data:city, timestamp=1702246030940, value=C\xC3\xB3rdoba
 1                                       column=personal_data:name, timestamp=1702246023992, value=Juan
 2                                       column=personal_data:age, timestamp=1702246072901, value=32
 2                                       column=personal_data:city, timestamp=1702246050411, value=Lima
 2                                       column=personal_data:name, timestamp=1702246044175, value=Franco
 3                                       column=personal_data:age, timestamp=1702246086423, value=34
 3                                       column=personal_data:name, timestamp=1702246079672, value=Ivan
 4                                       column=personal_data:city, timestamp=1702246098371, value=Caracas
 4                                       column=personal_data:name, timestamp=1702246092675, value=Eliecer
 5                                       column=personal_data:age, timestamp=1702246214228, value=24
 5                                       column=personal_data:city, timestamp=1702246214228, value=Buenos Aires
 5                                       column=personal_data:name, timestamp=1702246214228, value=Olivia
 6                                       column=personal_data:age, timestamp=1702246214228, value=27
 6                                       column=personal_data:city, timestamp=1702246214228, value=Buenos Aires
 6                                       column=personal_data:name, timestamp=1702246214228, value=Juliana
 7                                       column=personal_data:age, timestamp=1702246214228, value=26
 7                                       column=personal_data:city, timestamp=1702246214228, value=Mexico DF
 7                                       column=personal_data:name, timestamp=1702246214228, value=Orlando
 8                                       column=personal_data:age, timestamp=1702246214228, value=30
 8                                       column=personal_data:city, timestamp=1702246214228, value=Ontario
 8                                       column=personal_data:name, timestamp=1702246214228, value=Ricardo
8 row(s) in 0.3220 seconds

hbase(main):002:0> create 'album','label','image'

ERROR: Table already exists: album!

Here is some help for this command:
Creates a table. Pass a table name, and a set of column family
specifications (at least one), and, optionally, table configuration.
Column specification can be a simple string (name), or a dictionary
(dictionaries are described below in main help output), necessarily
including NAME attribute.
Examples:

Create a table with namespace=ns1 and table qualifier=t1
  hbase> create 'ns1:t1', {NAME => 'f1', VERSIONS => 5}

Create a table with namespace=default and table qualifier=t1
  hbase> create 't1', {NAME => 'f1'}, {NAME => 'f2'}, {NAME => 'f3'}
  hbase> # The above in shorthand would be the following:
  hbase> create 't1', 'f1', 'f2', 'f3'
  hbase> create 't1', {NAME => 'f1', VERSIONS => 1, TTL => 2592000, BLOCKCACHE => true}
  hbase> create 't1', {NAME => 'f1', CONFIGURATION => {'hbase.hstore.blockingStoreFiles' => '10'}}

Table configuration options can be put at the end.
Examples:

  hbase> create 'ns1:t1', 'f1', SPLITS => ['10', '20', '30', '40']
  hbase> create 't1', 'f1', SPLITS => ['10', '20', '30', '40']
  hbase> create 't1', 'f1', SPLITS_FILE => 'splits.txt', OWNER => 'johndoe'
  hbase> create 't1', {NAME => 'f1', VERSIONS => 5}, METADATA => { 'mykey' => 'myvalue' }
  hbase> # Optionally pre-split the table into NUMREGIONS, using
  hbase> # SPLITALGO ("HexStringSplit", "UniformSplit" or classname)
  hbase> create 't1', 'f1', {NUMREGIONS => 15, SPLITALGO => 'HexStringSplit'}
  hbase> create 't1', 'f1', {NUMREGIONS => 15, SPLITALGO => 'HexStringSplit', REGION_REPLICATION => 2, CONFIGURATION => {'hbase.hregion.scan.loadColumnFamiliesOnDemand' => 'true'}}
  hbase> create 't1', {NAME => 'f1', DFS_REPLICATION => 1}

You can also keep around a reference to the created table:

  hbase> t1 = create 't1', 'f1'

Which gives you a reference to the table named 't1', on which you can then
call methods.


hbase(main):003:0> put 'album','label1','label:size','10'
0 row(s) in 0.0640 seconds

hbase(main):004:0> put 'album','label1','label:color','255:255:255'
0 row(s) in 0.0170 seconds

hbase(main):005:0> put 'album','label1','label:text','Family album'
0 row(s) in 0.0160 seconds

hbase(main):006:0> put 'album','label1','image:name','holiday'
0 row(s) in 0.0150 seconds

hbase(main):007:0> put 'album','label1','image:source','/tmp/pic1.jpg'
0 row(s) in 0.0170 seconds

hbase(main):008:0> get 'album','label1'
COLUMN                                   CELL
 image:name                              timestamp=1702246293954, value=holiday
 image:source                            timestamp=1702246299934, value=/tmp/pic1.jpg
 label:color                             timestamp=1702246277549, value=255:255:255
 label:size                              timestamp=1702246270938, value=10
 label:text                              timestamp=1702246286343, value=Family album
5 row(s) in 0.0490 seconds
```
salimos del shell con Ctrl+DF


B) MongoDB

Me muevo a la carpeta Datasets y copiamos los archivos iris.csv e iris.json
```
adminstaller@Labo-AZ10:~/herramientas_big_data$ cd Datasets/
adminstaller@Labo-AZ10:~/herramientas_big_data/Datasets$ sudo docker cp iris.csv mongodb:/data/iris.csv
Successfully copied 6.66kB to mongodb:/data/iris.csv
adminstaller@Labo-AZ10:~/herramientas_big_data/Datasets$ sudo docker cp iris.json mongodb:/data/iris.json
Successfully copied 17.4kB to mongodb:/data/iris.json
adminstaller@Labo-AZ10:~/herramientas_big_data/Datasets$
```
Luego me voy al shell de mongodb e importo
```
adminstaller@Labo-AZ10:~/herramientas_big_data/Datasets$ sudo docker exec -it mongodb bash
root@86dcf5a8a344:/# mongoimport /data/iris.csv --type csv --headerline -d dataprueba -c iris_csv
2023-12-10T22:13:34.649+0000    connected to: mongodb://localhost/
2023-12-10T22:13:34.723+0000    150 document(s) imported successfully. 0 document(s) failed to import.
root@86dcf5a8a344:/# mongoimport --db dataprueba --collection iris_json --file /data/iris.json --jsonArray
2023-12-10T22:13:45.258+0000    connected to: mongodb://localhost/
2023-12-10T22:13:45.273+0000    150 document(s) imported successfully. 0 document(s) failed to import.
```
ejecuto mogosh y ejecuto lo propuesto en el readme
```
root@86dcf5a8a344:/# mongosh
Current Mongosh Log ID: 6576383bf97e789596c8fb4f
Connecting to:          mongodb://127.0.0.1:27017/?directConnection=true&serverSelectionTimeoutMS=2000&appName=mongosh+2.1.0
Using MongoDB:          7.0.4
Using Mongosh:          2.1.0

For mongosh info see: https://docs.mongodb.com/mongodb-shell/

------
   The server generated these startup warnings when booting
   2023-12-09T20:05:21.338+00:00: Using the XFS filesystem is strongly recommended with the WiredTiger storage engine. See http://dochub.mongodb.org/core/prodnotes-filesystem
   2023-12-09T20:05:23.974+00:00: Access control is not enabled for the database. Read and write access to data and configuration is unrestricted
   2023-12-09T20:05:23.974+00:00: /sys/kernel/mm/transparent_hugepage/enabled is 'always'. We suggest setting it to 'never'
   2023-12-09T20:05:23.974+00:00: vm.max_map_count is too low
------

test> use dataprueba
switched to db dataprueba
dataprueba> show collections
iris_csv
iris_json
dataprueba> db.iris_csv.find()
[
  {
    _id: ObjectId('6574d119c2fcc5514cf04861'),
    fila: 'fila1',
    sepal_length: 5.1,
    sepal_width: 3.5,
    petal_length: 1.4,
    petal_width: 0.2,
    species: 'setosa'
  },
  {
    _id: ObjectId('6574d119c2fcc5514cf04862'),
    fila: 'fila2',
    sepal_length: 4.9,
    sepal_width: 3,
    petal_length: 1.4,
    petal_width: 0.2,
    species: 'setosa'
  },
  {
    _id: ObjectId('6574d119c2fcc5514cf04863'),
    fila: 'fila3',
    sepal_length: 4.7,
    sepal_width: 3.2,
    petal_length: 1.3,
    petal_width: 0.2,
    species: 'setosa'
  },
  {
    _id: ObjectId('6574d119c2fcc5514cf04864'),
    fila: 'fila4',
    sepal_length: 4.6,
    sepal_width: 3.1,
    petal_length: 1.5,
    petal_width: 0.2,
    species: 'setosa'
  },
  {
    _id: ObjectId('6574d119c2fcc5514cf04865'),
    fila: 'fila5',
    sepal_length: 5,
    sepal_width: 3.6,
    petal_length: 1.4,
    petal_width: 0.2,
    species: 'setosa'
  },
  {
    _id: ObjectId('6574d119c2fcc5514cf04866'),
    fila: 'fila6',
    sepal_length: 5.4,
    sepal_width: 3.9,
    petal_length: 1.7,
    petal_width: 0.4,
    species: 'setosa'
  },
  {
    _id: ObjectId('6574d119c2fcc5514cf04867'),
    fila: 'fila7',
    sepal_length: 4.6,
    sepal_width: 3.4,
    petal_length: 1.4,
    petal_width: 0.3,
    species: 'setosa'
  },
  {
    _id: ObjectId('6574d119c2fcc5514cf04868'),
    fila: 'fila8',
    sepal_length: 5,
    sepal_width: 3.4,
    petal_length: 1.5,
    petal_width: 0.2,
    species: 'setosa'
  },
  {
    _id: ObjectId('6574d119c2fcc5514cf04869'),
    fila: 'fila9',
    sepal_length: 4.4,
    sepal_width: 2.9,
    petal_length: 1.4,
    petal_width: 0.2,
    species: 'setosa'
  },
  {
    _id: ObjectId('6574d119c2fcc5514cf0486a'),
    fila: 'fila10',
    sepal_length: 4.9,
    sepal_width: 3.1,
    petal_length: 1.5,
    petal_width: 0.1,
    species: 'setosa'
  },
  {
    _id: ObjectId('6574d119c2fcc5514cf0486b'),
    fila: 'fila11',
    sepal_length: 5.4,
    sepal_width: 3.7,
    petal_length: 1.5,
    petal_width: 0.2,
    species: 'setosa'
  },
  {
    _id: ObjectId('6574d119c2fcc5514cf0486c'),
    fila: 'fila12',
    sepal_length: 4.8,
    sepal_width: 3.4,
    petal_length: 1.6,
    petal_width: 0.2,
    species: 'setosa'
  },
  {
    _id: ObjectId('6574d119c2fcc5514cf0486d'),
    fila: 'fila13',
    sepal_length: 4.8,
    sepal_width: 3,
    petal_length: 1.4,
    petal_width: 0.1,
    species: 'setosa'
  },
  {
    _id: ObjectId('6574d119c2fcc5514cf0486e'),
    fila: 'fila14',
    sepal_length: 4.3,
    sepal_width: 3,
    petal_length: 1.1,
    petal_width: 0.1,
    species: 'setosa'
  },
  {
    _id: ObjectId('6574d119c2fcc5514cf0486f'),
    fila: 'fila15',
    sepal_length: 5.8,
    sepal_width: 4,
    petal_length: 1.2,
    petal_width: 0.2,
    species: 'setosa'
  },
  {
    _id: ObjectId('6574d119c2fcc5514cf04870'),
    fila: 'fila16',
    sepal_length: 5.7,
    sepal_width: 4.4,
    petal_length: 1.5,
    petal_width: 0.4,
    species: 'setosa'
  },
  {
    _id: ObjectId('6574d119c2fcc5514cf04871'),
    fila: 'fila17',
    sepal_length: 5.4,
    sepal_width: 3.9,
    petal_length: 1.3,
    petal_width: 0.4,
    species: 'setosa'
  },
  {
    _id: ObjectId('6574d119c2fcc5514cf04872'),
    fila: 'fila18',
    sepal_length: 5.1,
    sepal_width: 3.5,
    petal_length: 1.4,
    petal_width: 0.3,
    species: 'setosa'
  },
  {
    _id: ObjectId('6574d119c2fcc5514cf04873'),
    fila: 'fila19',
    sepal_length: 5.7,
    sepal_width: 3.8,
    petal_length: 1.7,
    petal_width: 0.3,
    species: 'setosa'
  },
  {
    _id: ObjectId('6574d119c2fcc5514cf04874'),
    fila: 'fila20',
    sepal_length: 5.1,
    sepal_width: 3.8,
    petal_length: 1.5,
    petal_width: 0.3,
    species: 'setosa'
  }
]
Type "it" for more
dataprueba> db.iris_json.find()
[
  {
    _id: ObjectId('6574d12165d0541c5f7b2dad'),
    sepalLength: 5.1,
    sepalWidth: 3.5,
    petalLength: 1.4,
    petalWidth: 0.2,
    species: 'setosa'
  },
  {
    _id: ObjectId('6574d12165d0541c5f7b2dae'),
    sepalLength: 4.9,
    sepalWidth: 3,
    petalLength: 1.4,
    petalWidth: 0.2,
    species: 'setosa'
  },
  {
    _id: ObjectId('6574d12165d0541c5f7b2daf'),
    sepalLength: 4.7,
    sepalWidth: 3.2,
    petalLength: 1.3,
    petalWidth: 0.2,
    species: 'setosa'
  },
  {
    _id: ObjectId('6574d12165d0541c5f7b2db0'),
    sepalLength: 4.6,
    sepalWidth: 3.1,
    petalLength: 1.5,
    petalWidth: 0.2,
    species: 'setosa'
  },
  {
    _id: ObjectId('6574d12165d0541c5f7b2db1'),
    sepalLength: 5,
    sepalWidth: 3.6,
    petalLength: 1.4,
    petalWidth: 0.2,
    species: 'setosa'
  },
  {
    _id: ObjectId('6574d12165d0541c5f7b2db2'),
    sepalLength: 4.6,
    sepalWidth: 3.4,
    petalLength: 1.4,
    petalWidth: 0.3,
    species: 'setosa'
  },
  {
    _id: ObjectId('6574d12165d0541c5f7b2db3'),
    sepalLength: 5.4,
    sepalWidth: 3.9,
    petalLength: 1.7,
    petalWidth: 0.4,
    species: 'setosa'
  },
  {
    _id: ObjectId('6574d12165d0541c5f7b2db4'),
    sepalLength: 5,
    sepalWidth: 3.4,
    petalLength: 1.5,
    petalWidth: 0.2,
    species: 'setosa'
  },
  {
    _id: ObjectId('6574d12165d0541c5f7b2db5'),
    sepalLength: 4.4,
    sepalWidth: 2.9,
    petalLength: 1.4,
    petalWidth: 0.2,
    species: 'setosa'
  },
  {
    _id: ObjectId('6574d12165d0541c5f7b2db6'),
    sepalLength: 4.9,
    sepalWidth: 3.1,
    petalLength: 1.5,
    petalWidth: 0.1,
    species: 'setosa'
  },
  {
    _id: ObjectId('6574d12165d0541c5f7b2db7'),
    sepalLength: 4.8,
    sepalWidth: 3.4,
    petalLength: 1.6,
    petalWidth: 0.2,
    species: 'setosa'
  },
  {
    _id: ObjectId('6574d12165d0541c5f7b2db8'),
    sepalLength: 4.8,
    sepalWidth: 3,
    petalLength: 1.4,
    petalWidth: 0.1,
    species: 'setosa'
  },
  {
    _id: ObjectId('6574d12165d0541c5f7b2db9'),
    sepalLength: 4.3,
    sepalWidth: 3,
    petalLength: 1.1,
    petalWidth: 0.1,
    species: 'setosa'
  },
  {
    _id: ObjectId('6574d12165d0541c5f7b2dba'),
    sepalLength: 5.8,
    sepalWidth: 4,
    petalLength: 1.2,
    petalWidth: 0.2,
    species: 'setosa'
  },
  {
    _id: ObjectId('6574d12165d0541c5f7b2dbb'),
    sepalLength: 5.7,
    sepalWidth: 4.4,
    petalLength: 1.5,
    petalWidth: 0.4,
    species: 'setosa'
  },
  {
    _id: ObjectId('6574d12165d0541c5f7b2dbc'),
    sepalLength: 5.4,
    sepalWidth: 3.7,
    petalLength: 1.5,
    petalWidth: 0.2,
    species: 'setosa'
  },
  {
    _id: ObjectId('6574d12165d0541c5f7b2dbd'),
    sepalLength: 5.1,
    sepalWidth: 3.5,
    petalLength: 1.4,
    petalWidth: 0.3,
    species: 'setosa'
  },
  {
    _id: ObjectId('6574d12165d0541c5f7b2dbe'),
    sepalLength: 5.4,
    sepalWidth: 3.9,
    petalLength: 1.3,
    petalWidth: 0.4,
    species: 'setosa'
  },
  {
    _id: ObjectId('6574d12165d0541c5f7b2dbf'),
    sepalLength: 5.7,
    sepalWidth: 3.8,
    petalLength: 1.7,
    petalWidth: 0.3,
    species: 'setosa'
  },
  {
    _id: ObjectId('6574d12165d0541c5f7b2dc0'),
    sepalLength: 5.1,
    sepalWidth: 3.8,
    petalLength: 1.5,
    petalWidth: 0.3,
    species: 'setosa'
  }
]
Type "it" for more
```
Vuelvo al shell de mongodb y ejecuto para exportar y escapo

```
root@86dcf5a8a344:/# mongoexport --db dataprueba --collection iris_csv --fields sepal_length,sepal_width,petal_length,petal_width,species --type=csv --out /data/iris_export.csv
2023-12-10T22:22:51.535+0000    connected to: mongodb://localhost/
2023-12-10T22:22:51.554+0000    exported 300 records
root@86dcf5a8a344:/# mongoexport --db dataprueba --collection iris_json --fields sepal_length,sepal_width,petal_length,petal_width,species --type=json --out /data/iris_export.json
2023-12-10T22:23:13.175+0000    connected to: mongodb://localhost/
2023-12-10T22:23:13.183+0000    exported 300 records
root@86dcf5a8a344:/exit
```
Me posiciono en la carpeta Mongo y copio los archivos .jar
```
adminstaller@Labo-AZ10:~/herramientas_big_data$ cd Mongo/
adminstaller@Labo-AZ10:~/herramientas_big_data/Mongo$ sudo docker cp mongo-hadoop-hive-2.0.2.jar hive-server:/opt/hive/lib/mongo-hadoop-hive-2.0.2.jar
Successfully copied 30.2kB to hive-server:/opt/hive/lib/mongo-hadoop-hive-2.0.2.jar
adminstaller@Labo-AZ10:~/herramientas_big_data/Mongo$ sudo docker cp mongo-hadoop-core-2.0.2.jar hive-server:/opt/hive/lib/mongo-hadoop-core-2.0.2.jar
Successfully copied 142kB to hive-server:/opt/hive/lib/mongo-hadoop-core-2.0.2.jar
adminstaller@Labo-AZ10:~/herramientas_big_data/Mongo$ sudo docker cp mongo-hadoop-spark-2.0.2.jar hive-server:/opt/hive/lib/mongo-hadoop-spark-2.0.2.jar
Successfully copied 1.65MB to hive-server:/opt/hive/lib/mongo-hadoop-spark-2.0.2.jar
adminstaller@Labo-AZ10:~/herramientas_big_data/Mongo$ sudo docker cp mongo-java-driver-3.12.11.jar hive-server:/opt/hive/lib/mongo-java-driver-3.12.11.jar
Successfully copied 2.32MB to hive-server:/opt/hive/lib/mongo-java-driver-3.12.11.jar
adminstaller@Labo-AZ10:~/herramientas_big_data/Mongo$
```
Subo un directorio de la carpeta y copio el archivo iris.hql me voy al shell de hive e inicio HiveServer2, para darle permisos 777 al archivo 
iris.hql
```
adminstaller@Labo-AZ10:~/herramientas_big_data/Mongo$ cd ..
adminstaller@Labo-AZ10:~/herramientas_big_data$ sudo docker cp iris.hql hive-server:/opt/iris.hql
Successfully copied 2.56kB to hive-server:/opt/iris.hql
adminstaller@Labo-AZ10:~/herramientas_big_data$ sudo docker exec -it hive-server bash
root@67bd040ac32b:/opt# hiveserver2
2023-12-10 22:26:08: Starting HiveServer2
SLF4J: Class path contains multiple SLF4J bindings.
SLF4J: Found binding in [jar:file:/opt/hive/lib/log4j-slf4j-impl-2.6.2.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: Found binding in [jar:file:/opt/hadoop-2.7.4/share/hadoop/common/lib/slf4j-log4j12-1.7.10.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: See http://www.slf4j.org/codes.html#multiple_bindings for an explanation.
SLF4J: Actual binding is of type [org.apache.logging.slf4j.Log4jLoggerFactory]
root@67bd040ac32b:/opt# chmod 777 iris.hql
root@67bd040ac32b:/opt# hive -f iris.hql
SLF4J: Class path contains multiple SLF4J bindings.
SLF4J: Found binding in [jar:file:/opt/hive/lib/log4j-slf4j-impl-2.6.2.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: Found binding in [jar:file:/opt/hadoop-2.7.4/share/hadoop/common/lib/slf4j-log4j12-1.7.10.jar!/org/slf4j/impl/StaticLoggerBinder.class]
SLF4J: See http://www.slf4j.org/codes.html#multiple_bindings for an explanation.
SLF4J: Actual binding is of type [org.apache.logging.slf4j.Log4jLoggerFactory]

Logging initialized using configuration in file:/opt/hive/conf/hive-log4j2.properties Async: true
File does not exist: hdfs://namenode:9000/tmp/udfs/mongo-java-driver-3.12.11.jar
Query returned non-zero code: 1, cause: java.io.FileNotFoundException: File does not exist: hdfs://namenode:9000/tmp/udfs/mongo-java-driver-3.12.11.jar
root@67bd040ac32b:/opt#exit
```
6) Spark

1) Spark y Scala: Ejecuto comandos del Spark master y comenzar PySpark.
```
adminstaller@Labo-AZ10:~/herramientas_big_data$ docker exec -it spark-master bash
permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get "http://%2Fvar%2Frun%2Fdocker.sock/v1.24/containers/spark-master/json": dial unix /var/run/docker.sock: connect: permission denied
adminstaller@Labo-AZ10:~/herramientas_big_data$ sudo docker exec -it spark-master bash
bash-5.0# /spark/bin/pyspark --master spark://spark-master:7077
Python 2.7.18 (default, May  3 2020, 22:58:12)
[GCC 8.3.0] on linux2
Type "help", "copyright", "credits" or "license" for more information.
23/12/11 03:55:58 WARN NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable
Using Spark's default log4j profile: org/apache/spark/log4j-defaults.properties
Setting default log level to "WARN".
To adjust logging level use sc.setLogLevel(newLevel). For SparkR, use setLogLevel(newLevel).
/spark/python/pyspark/context.py:220: DeprecationWarning: Support for Python 2 and Python 3 prior to version 3.6 is deprecated as of Spark 3.0. See also the plan for dropping Python 2 support at https://spark.apache.org/news/plan-for-dropping-python-2-support.html.
  DeprecationWarning)
Welcome to
      ____              __
     / __/__  ___ _____/ /__
    _\ \/ _ \/ _ `/ __/  '_/
   /__ / .__/\_,_/_/ /_/\_\   version 3.0.0
      /_/

Using Python version 2.7.18 (default, May  3 2020 22:58:12)
SparkSession available as 'spark'.
>>> from pyspark.sql.types import *
>>> flightSchema = StructType([
...     StructField("DayofMonth", IntegerType(), False),
...     StructField("DayOfWeek", IntegerType(), False),
...     StructField("Carrier", StringType(), False),
...     StructField("OriginAirportID", IntegerType(), False),
...     StructField("DestAirportID", IntegerType(), False),
...     StructField("DepDelay", IntegerType(), False),
...     StructField("ArrDelay", IntegerType(), False),
...     ]);
```
En este punto el readme sugiere ejecutar flights = spark.read.csv('hdfs://namenode:9000/data/flights/raw-flight-data.csv', schema=flightSchema, 
header=True) pero esto no se encuentra en dicho directorio, si no en
 ``` 
>>> flights = spark.read.csv('hdfs://namenode:9000/data/Datasets/raw-flight-data.csv', schema=flightSchema, header=True)
>>> flights.show()
+----------+---------+-------+---------------+-------------+--------+--------+
|DayofMonth|DayOfWeek|Carrier|OriginAirportID|DestAirportID|DepDelay|ArrDelay|
+----------+---------+-------+---------------+-------------+--------+--------+
|        19|        5|     DL|          11433|        13303|      -3|       1|
|        19|        5|     DL|          14869|        12478|       0|      -8|
|        19|        5|     DL|          14057|        14869|      -4|     -15|
|        19|        5|     DL|          15016|        11433|      28|      24|
|        19|        5|     DL|          11193|        12892|      -6|     -11|
|        19|        5|     DL|          10397|        15016|      -1|     -19|
|        19|        5|     DL|          15016|        10397|       0|      -1|
|        19|        5|     DL|          10397|        14869|      15|      24|
|        19|        5|     DL|          10397|        10423|      33|      34|
|        19|        5|     DL|          11278|        10397|     323|     322|
|        19|        5|     DL|          14107|        13487|      -7|     -13|
|        19|        5|     DL|          11433|        11298|      22|      41|
|        19|        5|     DL|          11298|        11433|      40|      20|
|        19|        5|     DL|          11433|        12892|      -2|      -7|
|        19|        5|     DL|          10397|        12451|      71|      75|
|        19|        5|     DL|          12451|        10397|      75|      57|
|        19|        5|     DL|          12953|        10397|      -1|      10|
|        19|        5|     DL|          11433|        12953|      -3|     -10|
|        19|        5|     DL|          10397|        14771|      31|      38|
|        19|        5|     DL|          13204|        10397|       8|      25|
+----------+---------+-------+---------------+-------------+--------+--------+
only showing top 20 rows

>>> flights.describe()
DataFrame[summary: string, DayofMonth: string, DayOfWeek: string, Carrier: string, OriginAirportID: string, DestAirportID: string, DepDelay: string, ArrDelay: string]
>>>
```
Ejecuto comandos del Spark master y comenzar Scala.
```
adminstaller@Labo-AZ10:~/herramientas_big_data$ sudo docker exec -it spark-master bash
bash-5.0# spark/bin/spark-shell --master spark://spark-master:7077
23/12/11 04:04:01 WARN NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable
Using Spark's default log4j profile: org/apache/spark/log4j-defaults.properties
Setting default log level to "WARN".
To adjust logging level use sc.setLogLevel(newLevel). For SparkR, use setLogLevel(newLevel).
Spark context Web UI available at http://9d5afd3320a3:4040
Spark context available as 'sc' (master = spark://spark-master:7077, app id = app-20231211040411-0001).
Spark session available as 'spark'.
Welcome to
      ____              __
     / __/__  ___ _____/ /__
    _\ \/ _ \/ _ `/ __/  '_/
   /___/ .__/\_,_/_/ /_/\_\   version 3.0.0
      /_/

Using Scala version 2.12.10 (OpenJDK 64-Bit Server VM, Java 1.8.0_252)
Type in expressions to have them evaluated.
Type :help for more information.

scala> case class flightSchema(DayofMonth:String, DayOfWeek:String, Carrier:String, OriginAirportID:String, DestAirportID:String, DepDelay:String, ArrDelay:String)
defined class flightSchema
```
En este punto el readme sugiere ejecutar val flights = spark.read.format("csv").option("sep", ",").option("header", "true").
load("hdfs://namenode:9000/data/flights/raw-flight-data.csv").as[flightSchema]pero esto no se encuentra en dicho directorio, si no en
```
scala> val flights = spark.read.format("csv").option("sep", ",").option("header", "true").load("hdfs://namenode:9000/data/Datasets/raw-flight-data.csv").as[flightSchema]
flights: org.apache.spark.sql.Dataset[flightSchema] = [DayofMonth: string, DayOfWeek: string ... 5 more fields]

scala> flights.show()
+----------+---------+-------+---------------+-------------+--------+--------+
|DayofMonth|DayOfWeek|Carrier|OriginAirportID|DestAirportID|DepDelay|ArrDelay|
+----------+---------+-------+---------------+-------------+--------+--------+
|        19|        5|     DL|          11433|        13303|      -3|       1|
|        19|        5|     DL|          14869|        12478|       0|      -8|
|        19|        5|     DL|          14057|        14869|      -4|     -15|
|        19|        5|     DL|          15016|        11433|      28|      24|
|        19|        5|     DL|          11193|        12892|      -6|     -11|
|        19|        5|     DL|          10397|        15016|      -1|     -19|
|        19|        5|     DL|          15016|        10397|       0|      -1|
|        19|        5|     DL|          10397|        14869|      15|      24|
|        19|        5|     DL|          10397|        10423|      33|      34|
|        19|        5|     DL|          11278|        10397|     323|     322|
|        19|        5|     DL|          14107|        13487|      -7|     -13|
|        19|        5|     DL|          11433|        11298|      22|      41|
|        19|        5|     DL|          11298|        11433|      40|      20|
|        19|        5|     DL|          11433|        12892|      -2|      -7|
|        19|        5|     DL|          10397|        12451|      71|      75|
|        19|        5|     DL|          12451|        10397|      75|      57|
|        19|        5|     DL|          12953|        10397|      -1|      10|
|        19|        5|     DL|          11433|        12953|      -3|     -10|
|        19|        5|     DL|          10397|        14771|      31|      38|
|        19|        5|     DL|          13204|        10397|       8|      25|
+----------+---------+-------+---------------+-------------+--------+--------+
only showing top 20 rows
```

B) Kafka

Este punto no pude ejecutarlo dado que al intentar conectar con bootstrap-server nos da timeout la consola, dejo evidencia.

```
adminstaller@Labo-AZ10:~/herramientas_big_data$ sudo docker exec -it kafka_container bash
bash-4.4# cd /opt/kafka/bin
bash-4.4# sh kafka-topics.sh --create --bootstrap-server kafka:9092 --replication-factor 1 --partitions 100 --topic demo
Error while executing topic command : Topic demo already exists
[2023-12-11 04:07:45,532] ERROR java.lang.IllegalArgumentException: Topic demo already exists
        at kafka.admin.TopicCommand$AdminClientTopicService.createTopic(TopicCommand.scala:177)
        at kafka.admin.TopicCommand$TopicService.createTopic(TopicCommand.scala:134)
        at kafka.admin.TopicCommand$TopicService.createTopic$(TopicCommand.scala:129)
        at kafka.admin.TopicCommand$AdminClientTopicService.createTopic(TopicCommand.scala:157)
        at kafka.admin.TopicCommand$.main(TopicCommand.scala:60)
        at kafka.admin.TopicCommand.main(TopicCommand.scala)
 (kafka.admin.TopicCommand$)
bash-4.4# sh kafka-topics.sh --list --bootstrap-server kafka:9092
demo
bash-4.4# sh kafka-topics.sh --describe --bootstrap-server kafka:9092 --topic demo
Error while executing topic command : org.apache.kafka.common.errors.TimeoutException: Timed out waiting to send the call.
[2023-12-11 04:11:17,444] ERROR java.util.concurrent.ExecutionException: org.apache.kafka.common.errors.TimeoutException: Timed out waiting to send the call.
        at org.apache.kafka.common.internals.KafkaFutureImpl.wrapAndThrow(KafkaFutureImpl.java:45)
        at org.apache.kafka.common.internals.KafkaFutureImpl.access$000(KafkaFutureImpl.java:32)
        at org.apache.kafka.common.internals.KafkaFutureImpl$SingleWaiter.await(KafkaFutureImpl.java:89)
        at org.apache.kafka.common.internals.KafkaFutureImpl.get(KafkaFutureImpl.java:260)
        at kafka.admin.TopicCommand$AdminClientTopicService.describeTopic(TopicCommand.scala:206)
        at kafka.admin.TopicCommand$.main(TopicCommand.scala:66)
        at kafka.admin.TopicCommand.main(TopicCommand.scala)
Caused by: org.apache.kafka.common.errors.TimeoutException: Timed out waiting to send the call.
 (kafka.admin.TopicCommand$)
bash-4.4#
```
C Comparativa Dataset y Dataframe en Scala: En este punto no pude avanzar dado que no encuentro la fuente de este errorm quizas este asociado 
con la falta de conecion del punto B
```
adminstaller@Labo-AZ10:~/herramientas_big_data$ sudo docker cp pruebaPySpark.py spark-master:pruebaPySpark.py
Successfully copied 3.07kB to spark-master:pruebaPySpark.py
adminstaller@Labo-AZ10:~/herramientas_big_data$ sudo docker cp pruebaScala.scala spark-master:pruebaScala.scala
Successfully copied 3.07kB to spark-master:pruebaScala.scala
adminstaller@Labo-AZ10:~/herramientas_big_data$ sudo docker exec -it spark-master bash
bash-5.0# /spark/bin/spark-submit --master spark://spark-master:7077 pruebaPySpark.py
23/12/11 04:22:07 WARN NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable
Using Spark's default log4j profile: org/apache/spark/log4j-defaults.properties
23/12/11 04:22:07 INFO SparkContext: Running Spark version 3.0.0
23/12/11 04:22:08 INFO ResourceUtils: ==============================================================
23/12/11 04:22:08 INFO ResourceUtils: Resources for spark.driver:

23/12/11 04:22:08 INFO ResourceUtils: ==============================================================
23/12/11 04:22:08 INFO SparkContext: Submitted application: prueba-pyspark
23/12/11 04:22:08 INFO SecurityManager: Changing view acls to: root
23/12/11 04:22:08 INFO SecurityManager: Changing modify acls to: root
23/12/11 04:22:08 INFO SecurityManager: Changing view acls groups to:
23/12/11 04:22:08 INFO SecurityManager: Changing modify acls groups to:
23/12/11 04:22:08 INFO SecurityManager: SecurityManager: authentication disabled; ui acls disabled; users  with view permissions: Set(root); groups with view permissions: Set(); users  with modify permissions: Set(root); groups with modify permissions: Set()
23/12/11 04:22:08 INFO Utils: Successfully started service 'sparkDriver' on port 34639.
23/12/11 04:22:08 INFO SparkEnv: Registering MapOutputTracker
23/12/11 04:22:08 INFO SparkEnv: Registering BlockManagerMaster
23/12/11 04:22:08 INFO BlockManagerMasterEndpoint: Using org.apache.spark.storage.DefaultTopologyMapper for getting topology information
23/12/11 04:22:08 INFO BlockManagerMasterEndpoint: BlockManagerMasterEndpoint up
23/12/11 04:22:08 INFO SparkEnv: Registering BlockManagerMasterHeartbeat
23/12/11 04:22:08 INFO DiskBlockManager: Created local directory at /tmp/blockmgr-b03b2d91-1937-423c-a6cb-9ee0b66eaf6a
23/12/11 04:22:08 INFO MemoryStore: MemoryStore started with capacity 366.3 MiB
23/12/11 04:22:08 INFO SparkEnv: Registering OutputCommitCoordinator
23/12/11 04:22:08 INFO Utils: Successfully started service 'SparkUI' on port 4040.
23/12/11 04:22:08 INFO SparkUI: Bound SparkUI to 0.0.0.0, and started at http://9d5afd3320a3:4040
23/12/11 04:22:09 INFO StandaloneAppClient$ClientEndpoint: Connecting to master spark://spark-master:7077...
23/12/11 04:22:09 INFO TransportClientFactory: Successfully created connection to spark-master/172.19.0.16:7077 after 38 ms (0 ms spent in bootstraps)
23/12/11 04:22:09 INFO StandaloneSchedulerBackend: Connected to Spark cluster with app ID app-20231211042209-0004
23/12/11 04:22:09 INFO StandaloneAppClient$ClientEndpoint: Executor added: app-20231211042209-0004/0 on worker-20231211035218-172.19.0.17-35943 (172.19.0.17:35943) with 2 core(s)
23/12/11 04:22:09 INFO StandaloneSchedulerBackend: Granted executor ID app-20231211042209-0004/0 on hostPort 172.19.0.17:35943 with 2 core(s), 512.0 MiB RAM
23/12/11 04:22:09 INFO Utils: Successfully started service 'org.apache.spark.network.netty.NettyBlockTransferService' on port 43921.
23/12/11 04:22:09 INFO NettyBlockTransferService: Server created on 9d5afd3320a3:43921
23/12/11 04:22:09 INFO BlockManager: Using org.apache.spark.storage.RandomBlockReplicationPolicy for block replication policy
23/12/11 04:22:09 INFO BlockManagerMaster: Registering BlockManager BlockManagerId(driver, 9d5afd3320a3, 43921, None)
23/12/11 04:22:09 INFO StandaloneAppClient$ClientEndpoint: Executor updated: app-20231211042209-0004/0 is now RUNNING
23/12/11 04:22:09 INFO BlockManagerMasterEndpoint: Registering block manager 9d5afd3320a3:43921 with 366.3 MiB RAM, BlockManagerId(driver, 9d5afd3320a3, 43921, None)
23/12/11 04:22:09 INFO BlockManagerMaster: Registered BlockManager BlockManagerId(driver, 9d5afd3320a3, 43921, None)
23/12/11 04:22:09 INFO BlockManager: Initialized BlockManager: BlockManagerId(driver, 9d5afd3320a3, 43921, None)
23/12/11 04:22:09 INFO StandaloneSchedulerBackend: SchedulerBackend is ready for scheduling beginning after reached minRegisteredResourcesRatio: 0.0
/spark/python/lib/pyspark.zip/pyspark/context.py:220: DeprecationWarning: Support for Python 2 and Python 3 prior to version 3.6 is deprecated as of Spark 3.0. See also the plan for dropping Python 2 support at https://spark.apache.org/news/plan-for-dropping-python-2-support.html.
  DeprecationWarning)
23/12/11 04:22:10 INFO SharedState: Setting hive.metastore.warehouse.dir ('null') to the value of spark.sql.warehouse.dir ('file:/spark-warehouse').
23/12/11 04:22:10 INFO SharedState: Warehouse path is 'file:/spark-warehouse'.
23/12/11 04:22:12 INFO ResourceProfile: Default ResourceProfile created, executor resources: Map(cores -> name: cores, amount: 1, script: , vendor: , memory -> name: memory, amount: 512, script: , vendor: ), task resources: Map(cpus -> name: cpus, amount: 1.0)
Traceback (most recent call last):
  File "/pruebaPySpark.py", line 26, in <module>
    flights = spark.read.csv('hdfs://namenode:9000/data/flights/raw-flight-data.csv', schema=flightSchema, header=True)
  File "/spark/python/lib/pyspark.zip/pyspark/sql/readwriter.py", line 535, in csv
  File "/spark/python/lib/py4j-0.10.9-src.zip/py4j/java_gateway.py", line 1305, in __call__
  File "/spark/python/lib/pyspark.zip/pyspark/sql/utils.py", line 137, in deco
  File "/spark/python/lib/pyspark.zip/pyspark/sql/utils.py", line 33, in raise_from
pyspark.sql.utils.AnalysisException: Path does not exist: hdfs://namenode:9000/data/flights/raw-flight-data.csv;
23/12/11 04:22:13 INFO SparkContext: Invoking stop() from shutdown hook
23/12/11 04:22:13 INFO SparkUI: Stopped Spark web UI at http://9d5afd3320a3:4040
23/12/11 04:22:13 INFO StandaloneSchedulerBackend: Shutting down all executors
23/12/11 04:22:13 INFO CoarseGrainedSchedulerBackend$DriverEndpoint: Asking each executor to shut down
23/12/11 04:22:13 INFO MapOutputTrackerMasterEndpoint: MapOutputTrackerMasterEndpoint stopped!
23/12/11 04:22:13 INFO MemoryStore: MemoryStore cleared
23/12/11 04:22:13 INFO BlockManager: BlockManager stopped
23/12/11 04:22:13 INFO BlockManagerMaster: BlockManagerMaster stopped
23/12/11 04:22:13 INFO OutputCommitCoordinator$OutputCommitCoordinatorEndpoint: OutputCommitCoordinator stopped!
23/12/11 04:22:13 INFO SparkContext: Successfully stopped SparkContext
23/12/11 04:22:13 INFO ShutdownHookManager: Shutdown hook called
23/12/11 04:22:13 INFO ShutdownHookManager: Deleting directory /tmp/spark-f0d93ae5-048d-46a9-8b6f-3285f85fbd44
23/12/11 04:22:13 INFO ShutdownHookManager: Deleting directory /tmp/spark-f0d93ae5-048d-46a9-8b6f-3285f85fbd44/pyspark-8f46ce1e-92df-41ef-8d5b-b570f6434406
23/12/11 04:22:13 INFO ShutdownHookManager: Deleting directory /tmp/spark-f6922083-e74f-48bf-aadf-359385e8c1e9
bash-5.0# /spark/bin/spark-shell --master spark://spark-master:7077 -i pruebaScala.scala
23/12/11 04:22:20 WARN NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable
Using Spark's default log4j profile: org/apache/spark/log4j-defaults.properties
Setting default log level to "WARN".
To adjust logging level use sc.setLogLevel(newLevel). For SparkR, use setLogLevel(newLevel).
Spark context Web UI available at http://9d5afd3320a3:4040
Spark context available as 'sc' (master = spark://spark-master:7077, app id = app-20231211042228-0005).
Spark session available as 'spark'.
pruebaScala.scala:1: error: ';' expected but identifier found.
import org.apache.spark::spark-sql:3.0.0
                       ^
Welcome to
      ____              __
     / __/__  ___ _____/ /__
    _\ \/ _ \/ _ `/ __/  '_/
   /___/ .__/\_,_/_/ /_/\_\   version 3.0.0
      /_/

Using Scala version 2.12.10 (OpenJDK 64-Bit Server VM, Java 1.8.0_252)
Type in expressions to have them evaluated.
Type :help for more information.

scala> /spark/bin/pyspark --master spark://spark-master:7077
     | /spark/bin/spark-shell --master spark://spark-master:7077
<console>:2: error: ';' expected but ':' found.
       /spark/bin/spark-shell --master spark://spark-master:7077
                                            ^

scala>
```
