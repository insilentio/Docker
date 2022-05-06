# Environment with Hadoop-Spark Cluster, Cassandra-DB and Jupyter Notbook

**needs Cassandra-Spark connector:**


SBT needs to be installed for this; container needs to be started as root (-- user root) for this. Then:

```
echo "deb https://dl.bintray.com/sbt/debian /" | sudo tee -a /etc/apt/sources.list.d/sbt.list
sudo apt-get install gnupg
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2EE0EA64E40A89B84B2DF73499E82A75642AC823
sudo apt-get update sudo apt-get install sbt
```

Now we can install the connector:

```
git clone https://github.com/anguenot/pyspark-cassandra.git
cd pyspark-cassandra
sbt compile
sbt spPublishLocal
```
