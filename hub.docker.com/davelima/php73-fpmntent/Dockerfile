FROM dav009/java-7
MAINTAINER David Przybilla <dav.alejandro@gmail.com>

ENV SPARK_VERSION "2.0.2"
ENV SPARK_PATH "/spark-${SPARK_VERSION}-bin-hadoop2.7"
ENV SPARK_FILE "spark-${SPARK_VERSION}-bin-hadoop2.7.tgz"

ENV SPARK_URL "http://mirror2.shellbot.com/apache/spark/spark-${SPARK_VERSION}/${SPARK_FILE}"

ADD $SPARK_URL /
RUN tar -xvf $SPARK_FILE
RUN ln -s $SPARK_PATH /var/lib/spark

RUN apt-get install -y python
RUN apt-get install -y python-pip 
