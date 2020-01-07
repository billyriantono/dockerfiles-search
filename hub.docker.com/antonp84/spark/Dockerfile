##########################################################################################
# Data Science toolbox with Spark 2.0:                                                   #
# - Essential set of R and Python packages from base image                               #
# - Spark 2.0                                                                            #
#                                                                                        #
# Usage:                                                                                 #
# import pyspark; sc = pyspark.SparkContext('local[*]')                                  #
#                                                                                        #
# v1.0, 15.08.2016                                                                       #
##########################################################################################

FROM antonp84/base

ENV SPARK_VERSION 2.0.0
ENV HADOOP_VERSION 2.7

# spark config
ENV SPARK_HOME  /opt/spark-2.0.0-bin-hadoop2.7
ENV PYTHONPATH $SPARK_HOME/python:$SPARK_HOME/python/lib/py4j-0.10.1-src.zip
ENV PYSPARK_PYTHON python3

# java
RUN apt-get update && \
	apt-get upgrade -y && \
	apt-get install -y default-jre

# spark
RUN cd /opt && \
	wget --no-verbose http://apache-mirror.rbc.ru/pub/apache/spark/spark-${SPARK_VERSION}/spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz && \
	tar -xzf spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz && \
	rm /opt/spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz
	


# clean up
RUN  rm -rf /var/lib/apt/lists/*


VOLUME /home
EXPOSE 8888 4040 18080 8080 8081 

# create jupyter notebook
CMD jupyter notebook --no-browser --port 8888 --ip=0.0.0.0 --notebook-dir=/home