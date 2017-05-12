# Big Data Hackathon by Slovak Telekom

## Environment setup

The hackathon setup consists of these elements:

* Team nodes
* Clouder CDH enterpirse cluster

## Environment Patterns

Each team has a private virtual server. All servers are in the same subnet and have access to the CDH cluster. Access to these servers are possible via a public address with a unique private and public key pair available for each team.

## Team nodes

Each team nodes is equipped with a set tools and configuration to access the environment. These tools are pre-installed on a private node for each team. Participating teams may use the server however they wish. The teamX user will have sudo privileges.

### Jupyter Notebooks

* launching Jupyter Notebooks with Python kernel and Pyspark connectivity

```bash
export PYSPARK_DRIVER_PYTHON=jupyter
export PYSPARK_DRIVER_PYTHON_OPTS="notebook --no-browser --ip=0.0.0.0 --allow-root"
pyspark2
```

* optionaly you can also switch to a R kernel


> it's recommended to run these commands in screen or tmux in case of loss of connectivity

### HDFS file Access

* basic Hadoop clients are configured on each team node
* to list your home directory on HDFS you can run the following command

```bash
hdfs dfs -ls /user/team<your team number>
```

* for more details check [Hadoop documention](https://hadoop.apache.org/docs/r2.7.3/hadoop-project-dist/hadoop-hdfs/HDFSCommands.html)

> An alternative option, which could be more attractive for web development is using webHSFD.

### Using Spark to access data in Hive Tables

* assuming you have pyspark2 shell running with SparkContext available, the code below reads the table content into a Spark DataFrame

```python
from pyspark.sql import HiveContext

df = sqlContext.sql("select * from database.table")
```

* for more details check the Spark [SQL documention](http://spark.apache.org/docs/latest/sql-programming-guide.html#hive-tables)

### Apache Kafka

* Apache kafka will run using the default Cloudera setup
* brokers will be listnening on port 9092
* zookeeper available on 2181
