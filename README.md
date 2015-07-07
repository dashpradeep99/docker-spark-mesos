# Introduction

Dockerfiler for spark run with mesos.
Build with 

* latest scipystack images to unlock pyspark power.
* spark 1.4.0
* mesos 0.22.1

[Deploy spark on mesos cluster with docker](https://spark.apache.org/docs/latest/running-on-mesos.html#mesos-docker-support)
[Ipython Scipystack Image](https://registry.hub.docker.com/u/ipython/scipystack/)

# How to use

Build Image

```bash
./build
```

Spark driver config in your $SPARK\_HOME/conf/spark-default.conf

```bash
spark.master                       mesos://your_mesos_master:5050
spark.mesos.mesosExecutor.cores    0.8
spark.mesos.executor.docker.image  sparkmesos:lastest
spark.mesos.executor.home          /opt/spark
```

Run the following script in any instance with mesos, docker installed to driver spark with mesos

```bash
docker run -it --rm \
  -e SPARK_MASTER="mesos://zk://$ZOOKEEPER_HOSTS" \
  -e SPARK_IMAGE="sparkmesos:1.0.0" \
  -e PYSPARK_DRIVER_PYTHON=ipython2 \
  sparkmesos:1.0.0 /opt/spark/bin/pyspark
```

# TODO

Add native netlib-java in the image for mllib. See [here](https://spark.apache.org/docs/latest/mllib-guide.html)