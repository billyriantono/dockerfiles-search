#############################################################
# Archivo Dockerfile para ejecutar apache STORM
# Basado en una imagen de Ubuntu
#############################################################

# Establece la imagen de base a utilizar para Ubuntu
FROM ubuntu:14.04

# Establece el autor (maintainer) del archivo (tu nombre - el autor del archivo)
MAINTAINER Mario <100292688@alumnos.uc3m.es>

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y  software-properties-common && \
    add-apt-repository ppa:webupd8team/java -y && \
    apt-get update && \
    echo oracle-java7-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections && \
    apt-get install -y oracle-java8-installer && \
    apt-get install -y git && \
    apt-get install -y maven && \
    apt-get install -y curl && \
    apt-get install -y build-essential && \
    apt-get clean

ENV STORM_VERSION 1.0.1
ENV ZOO_VERSION 3.4.8
ENV ZMQ_VERSION 4.1.5
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle/
ENV STORM_HOME /usr/local/src/apache-storm
RUN mkdir /var/stormtmp
RUN chmod 777 /var/stormtmp

# -- OBTENEMOS SOFTWARE PARA STORM -- #
RUN wget http://apache.rediris.es/zookeeper/zookeeper-$ZOO_VERSION/zookeeper-$ZOO_VERSION.tar.gz
RUN wget http://apache.rediris.es/storm/apache-storm-$STORM_VERSION/apache-storm-$STORM_VERSION.tar.gz
RUN wget https://github.com/zeromq/zeromq4-1/releases/download/v$ZMQ_VERSION/zeromq-$ZMQ_VERSION.tar.gz
RUN git clone https://github.com/zeromq/jzmq.git

RUN tar -xzvf zookeeper-$ZOO_VERSION.tar.gz -C /usr/local/src/
RUN tar -xzvf apache-storm-$STORM_VERSION.tar.gz -C /usr/local/src/
RUN tar -xzvf zeromq-$ZMQ_VERSION.tar.gz -C /usr/local/src/
RUN mv jzmq /usr/local/src/

RUN cp /usr/local/src/zookeeper-$ZOO_VERSION/conf/zoo_sample.cfg /usr/local/src/zookeeper-$ZOO_VERSION/conf/zoo.cfg
ADD storm.yaml /usr/local/src/apache-storm-$STORM_VERSION/conf/storm.yaml

RUN cd /usr/local/src/zeromq-$ZMQ_VERSION/ && ./configure
RUN cd /usr/local/src/zeromq-$ZMQ_VERSION/ && make
RUN cd /usr/local/src/zeromq-$ZMQ_VERSION/ && make install

RUN wget http://pkgconfig.freedesktop.org/releases/pkg-config-0.28.tar.gz
RUN apt-get install -y pkg-config
RUN apt-get install -y libtool
RUN apt-get install -y libboost-all-dev cmake flex
RUN apt-get install -y autoconf
#RUN tar -xzvf pkg-config-0.28.tar.gz -C /usr/local/src/
#RUN cd /usr/local/src/pkg-config-0.28 && ./configure
#RUN cd /usr/local/src/pkg-config-0.28 && make install

RUN cd /usr/local/src/jzmq/jzmq-jni/ && ./autogen.sh
RUN cd /usr/local/src/jzmq/jzmq-jni/ && ./configure
RUN cd /usr/local/src/jzmq/jzmq-jni/ && make
RUN cd /usr/local/src/jzmq/jzmq-jni/ && make install
RUN cd /usr/local/src/jzmq/ && mvn install -Dgpg.skip=true

RUN ln -s $STORM_HOME/bin/storm /usr/bin/storm

RUN cd /usr/local/src/apache-storm-$STORM_VERSION/examples/storm-starter/ && mvn eclipse:eclipse

#RUN /usr/local/src/zookeeper-$ZOO_VERSION/bin/zkServer.sh start
#RUN /usr/local/src/apache-storm-$STORM_VERSION/bin/storm nimbus&
#RUN /usr/local/src/apache-storm-$STORM_VERSION/bin/storm supervisor&



#/usr/local/src/apache-storm-$STORM_VERSION/bin/storm jar 
#/bigData/script/storm/storm-starter/target/storm-starter-0.10.0.jar 
#org.apache.storm.starter.WordCountTopology WordCount -c org.apache.storm.starter.WordCountTopology WordCount -c nimbus.host=localhost


#/usr/local/src/apache-storm-$STORM_VERSION/bin/storm jar /bigData/script/storm/storm-starter-1.0.1/target/storm-starter-1.0.1.jar org.apache.storm.starter.WordCountTopology WordCount -c org.apache.storm.starter.WordCountTopology WordCount -c nimbus.host=localhost



