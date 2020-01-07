# base
FROM asgard/base


###########################################################################
# Install Java.
# From official Oracle Java 8 Dockerfile
###########################################################################

RUN \
  echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
  add-apt-repository -y ppa:webupd8team/java && \
  apt-get  update && \
  apt-get install -y oracle-java8-installer && \
  rm -rf /var/cache/oracle-jdk8-installer

# Define commonly used JAVA_HOME variable
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle


###########################################################################
# Install Spark
# from https://github.com/gettyimages/docker-spark/blob/master/Dockerfile
###########################################################################

ENV SPARK_VERSION 1.6.3
ENV HADOOP_VERSION 2.6
ENV SPARK_PACKAGE $SPARK_VERSION-bin-hadoop$HADOOP_VERSION
ENV SPARK_HOME /usr/spark-$SPARK_PACKAGE
ENV PATH $PATH:$SPARK_HOME/bin
RUN curl -sL --retry 3 \
  "http://www-eu.apache.org/dist/spark/spark-$SPARK_VERSION/spark-$SPARK_PACKAGE.tgz" \
  | gunzip \
  | tar x -C /usr/ \
  && ln -s $SPARK_HOME /usr/spark

# ADD several jars for S3 connection, mysql...
RUN mkdir -p $SPARK_HOME/jars \
  && wget -P $SPARK_HOME/jars \
    "http://central.maven.org/maven2/com/amazonaws/aws-java-sdk/1.7.4/aws-java-sdk-1.7.4.jar" \
    "http://central.maven.org/maven2/org/apache/hadoop/hadoop-aws/2.7.1/hadoop-aws-2.7.1.jar" \
    "https://s3-eu-west-1.amazonaws.com/asgard-lib/directoutputcommiter_2.10-1.0.jar" \
    "http://central.maven.org/maven2/mysql/mysql-connector-java/5.1.38/mysql-connector-java-5.1.38.jar"

# Add conf file
ADD spark-defaults.conf $SPARK_HOME/conf/spark-defaults.conf
ADD hdfs-site.xml $SPARK_HOME/conf/hdfs-site.xml
ADD spark-env.sh $SPARK_HOME/conf/spark-env.sh

# create folder for history ui
RUN mkdir /tmp/spark-events


###########################################################################
# Init Setup Script
###########################################################################

# au cas ou
# RUN chmod +x init_script
ENTRYPOINT ["/sbin/init_script"]


###########################################################################
# Clean and Reduce image size
###########################################################################

RUN apt-get autoremove -y \
  && apt-get clean -y \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \