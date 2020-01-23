FROM wenzizone/base

RUN set -x; \
    apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -q -y git-core curl sudo xmlstarlet software-properties-common python-software-properties jq\
    && rm -rf /var/lib/apt/lists/*

# Install Java 8
RUN DEBIAN_FRONTEND=noninteractive apt-add-repository ppa:webupd8team/java -y
RUN apt-get update
RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections
RUN DEBIAN_FRONTEND=noninteractive apt-get install oracle-java8-installer -y
RUN rm -rf /var/lib/apt/lists/*


# Install HADOOP
ENV hadoop_ver 2.6.1
RUN mkdir -p /opt && \
    cd /opt && \
    curl http://www.us.apache.org/dist/hadoop/common/hadoop-${hadoop_ver}/hadoop-${hadoop_ver}.tar.gz | \
        tar -zx hadoop-${hadoop_ver}/lib/native && \
    ln -s hadoop-${hadoop_ver} hadoop && \
    echo Hadoop ${hadoop_ver} native libraries installed in /opt/hadoop/lib/native

# Install Spark
ENV SPARK_VERSION 1.6.0
ENV HADOOP_VERSION 2.6
ENV SPARK_PACKAGE spark-$SPARK_VERSION-bin-hadoop$HADOOP_VERSION
ENV SPARK_HOME /opt/$SPARK_PACKAGE
ENV PATH $PATH:$SPARK_HOME/bin
RUN curl -sL --retry 3 \
  "http://d3kbcqa49mib13.cloudfront.net/$SPARK_PACKAGE.tgz" \
  | gunzip \
  | tar x -C /opt/ \
  && ln -s $SPARK_HOME /opt/spark

ADD log4j.properties /opt/spark/conf/log4j.properties
ADD start-common.sh /
ADD spark-defaults.conf /opt/spark/conf/spark-defaults.conf
ENV PATH $PATH:/opt/spark/bin


ADD start.sh /
EXPOSE 7077 8080

CMD ["/start.sh"]


