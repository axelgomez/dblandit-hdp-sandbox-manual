# Iniciar y agregar al path HDFS y HIVE en hadoop sandbox

## Iniciar HDFS y YARN
- Correr desde la consola 
```
/home/hadoop/Desktop/curso/bin/start.sh
```

Deberá devolver algo similar a:
```
hadoop@hadoop-ml:~$ /home/hadoop/Desktop/curso/bin/start.sh
No arguments provided. Starting all daemons
Starting hadoop
Starting namenode...
namenode running as process 2429. Stop it first.
Starting datanode
datanode running as process 2476. Stop it first.
Starting yarn
Starting resourcemanager
resourcemanager running as process 2538. Stop it first.
Starting nodemanager
nodemanager running as process 2566. Stop it first.
Starting zookeeper
ZooKeeper JMX enabled by default
Using config: /home/hadoop/Desktop/curso/zookeeper-3.4.10/bin/../conf/zoo.cfg
Starting zookeeper ... already running as process 2631.
Starting spark
Starting master...
org.apache.spark.deploy.master.Master running as process 2659.  Stop it first.
Starting slave...
org.apache.spark.deploy.worker.Worker running as process 2711.  Stop it first.
```
Aquí ya se podrá interactuar con HDFS y HIVE

## Agregar binarios al path
Para poder correr los binarios de HDFS o HIVE (o cualquier otro que se prefiera) se deberá tener en el PATH de linux los directorios que incluyen esos binarios que queremos ejecutar.
Para que simplemente ejecutando `hdfs` o `hive` o cualquier binario que se utilice dentro de hadoop (`sqoop`, `pyspark`, etc....) se deberá comprobar si los binarios están dentro del PATH:
- En tal caso, al ejecutar:
```
hdfs
```

La salida será:
```
hadoop@hadoop-ml:~$ hdfs
Usage: hdfs [--config confdir] [--loglevel loglevel] COMMAND
       where COMMAND is one of:
  dfs                  run a filesystem command on the file systems supported in Hadoop.
  classpath            prints the classpath
  namenode -format     format the DFS filesystem
  secondarynamenode    run the DFS secondary namenode
  ...
```

- En caso contrario, si el error fuese:
```
hdfs: command not found
```
- ejecutar la siguiente linea por consola:
```
echo "export PATH=\$HADOOP_HOME/bin:\$HIVE_HOME/bin:\$PATH" >> ~/.bashrc
```

Activamos los cambios hechos al bashrc
```
source ~/.bashrc
```

Finalmente, ya se podrán ejecutar `hdfs` y `hive`

## Para agregar Pig
Ejecutar desde la consola:
```
cd ~/Desktop/curso/ && wget http://apache.dattatec.com/pig/pig-0.16.0/pig-0.16.0.tar.gz
tar -xvf pig-0.16.0.tar.gz
```

Ahora, agregamos el path del binario de pig:

```
echo "export PIG_HOME=/home/hadoop/Desktop/curso/pig-0.16.0" >> ~/.bashrc
echo "export PATH=\$PIG_HOME/bin:\$PATH" >> ~/.bashrc
```

Activamos los cambios hechos al bashrc
```
source ~/.bashrc
```

Finalmente, ya se podrá ejecutar `pig`


## Extras
Para saber si hdfs inició correctamente hay que dirigirse a la siguiente url en un navegador dentro de la máquina virtual:
[http://127.0.0.1:50070](http://127.0.0.1:50070)

O conociendo la IP de la máquina (por medio del comando `ifconfig` dentro de la virtual) dirigirse (desde la máquina local) a:
[http://<IP_maquina_virtual>:50070](http://<IP_maquina_virtual>:50070)
reemplazando <IP_maquina_virtual> por la IP correspondiente
