## Infraestructura BigData con Hadoop utilizando Docker Compose.
<br> En este contendeor podras encontrar HDFS, Hive, Spark, Hue, Zeppelin, Kafka, Zookeeper y NiFi
<br> Para la implementacion de este contenedor solo basta con descargar (clonar) este repositorio y, proceder a descomprimir en tu maquina local. 
<br> Luego, desde la linea de comando, ubicate sobre el directorio Hadoop y ejecuta `docker-compose up`

Este video explica como implementar BIG DATA en Amazon Web Services, en una máquina Linux (Ubuntu Server 20.04)

*************************
Comandos utilizados: (comando sudo puede omitirse si estas como usuario root)

sudo apt update
sudo apt upgrade
sudo apt-get install  curl apt-transport-https ca-certificates software-properties-common
curl -fsSL https://download.docker.com/linux/ubu... | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt update
sudo apt install docker-ce
sudo curl -L "https://github.com/docker/compose/rel... -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
sudo apt-get install git
sudo git clone https://github.com/juliopez/Hadoop.git
cd Hadoop
sudo docker-compose up -d

*****
Crear un archivo cualquiera por ejemplo: archivo.txt
*****
~/Hadoop$ sudo vi archivo.txt

Luego le pasé el archivo al contenedor NAMENODE con el comando Docker CP
~/Hadoop$ sudo docker cp archivo.txt namenode:/archivo.txt

Luego me conecté al contenedor NAMENODE de mi Docker
~/Hadoop$ sudo docker exec -it namenode bash

Dentro del contenedor creé el directorio hdfs "prueba" (esto dentro del contenedor NAMENODE de Docker)
/# hdfs dfs -mkdir /prueba

Luego distribuí el archivo con hdfs -put (esto dentro del contenedor NAMENODE de docker)
/# hdfs dfs -put archivo.txt /prueba/archivo.txt

y después verifiqué que el archivo se habia distribuido
/# hdfs dfs -ls /prueba

# ----

<br>Con esto completamos la instalación de Hadoop – HDFS -Spark -Hive- NiFi.
## Podemos comprobar la correcta ejecución de la siguiente forma. 
<br>En un browser ingresar a http://localhost: `numero de puerto`
<br>Donde <b>numero de puerto</b> puede ser:
<br>** 50070 (visualiza Hadoop y sus namenode)
<br>** 8080 (Spark Master)
<br>** 8081 (Spark  Worker)
<br>** 8888 (Hue. Se solicitará la creación de una cuenta. Ingrese admin como usuario y admin como password)
<br>** 9999 (NiFi)
<br>** 3030 (kafka)
<br>** 18630 (StreamSets. Utilice admin / admin)
<br>** 19090 (zeppelin)
### Para el uso de Hive 
<br> Ejecute en la consola `sudo docker exec -it hive-server bash`
<br> Luego ingrese al directorio donde esta alojado Hive, para esto deberá ejecutar el comando `cd /opt/hive/bin`
<br> Una vez dentro de dicho directorio, ejecute Hive con el siguiente comando  `./hive`
### Para el uso de mysql 
<br> Ejecute en la consola `sudo docker exec -it database bash`
<br> Luego el comando `mysql -h localhost -u root -p`
<br> Posterior a esto se solicitara la contraseña, la cual es : `secret`
### Para el uso de Spark (Scala)
<br> Ejecute en la consola `sudo docker exec -it spark-master bash`
<br> Luego ingrese al directorio donde esta alojado Spark, para esto deberá ejecutar el comando `cd /spark/bin`
<br> Una vez dentro de dicho directorio, ejecute Hive el siguiente comando  `./spark-shell`
### Para el uso de pyspark (Python)
<br> Ejecute en la consola `sudo docker exec -it spark-master bash`
<br> Luego ingrese al directorio donde esta alojado Spark, para esto deberá ejecutar el comando `cd /spark/bin`
<br> Una vez dentro de dicho directorio, ejecute el siguiente comando  `./pyspark`
### Para el uso de Kafka
<br> Ejecute en la consola `sudo docker exec -it kafka bash`
<br> Luego ingrese al directorio donde esta el productos y consumidor de Kafka, para esto deberá ejecutar el comando `cd /usr/local/bin`
<br> Para crear un TOPIC: `./kafka-topics  --create --zookeeper 172.27.1.15:2181 --replication-factor 1 --partitions 1 --topic EJEMPLO`
<br> Para verificar la creacion: `./kafka-topics --list --zookeeper 172.27.1.15:2181`
<br> Para crear un PRODUCTOR: `./kafka-console-producer --broker-list localhost:9092 --topic EJEMPLO`
<br> Para crear un CONSUMIDOR: `./kafka-console-consumer --bootstrap-server localhost:9092 --from-beginning --topic EJEMPLO`
<br>
<br>
<br> SI tienes problemas con HUE, mira la solucion propuesta aqui: [https://youtu.be/Ck4sRPa0o24](https://youtu.be/Ck4sRPa0o24)
<br>
<br> Si necesitas trabajar con sqoop, aqui una propuesta: [https://youtu.be/hLJFzOAbY8Q](https://youtu.be/hLJFzOAbY8Q)
<br>
<br> Mas info en [Blog de Julio Lopez-Nunez](https://juliopezblog.wordpress.com/).
