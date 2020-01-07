
				#############################################################
				# Archivo Dockerfile para ejecutar apache FLINK             #
				# Basado en una imagen de Ubuntu                            #
				#############################################################

# Establece la imagen de base a utilizar para Ubuntu
FROM ubuntu:14.04

# Establece el autor (maintainer) del archivo (tu nombre - el autor del archivo)
MAINTAINER Mario <100292688@alumnos.uc3m.es>

# Actualización de la lista de fuentes del repositorio de aplicaciones por defecto
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y  software-properties-common && \
    add-apt-repository ppa:webupd8team/java -y && \
    apt-get update && \
    echo oracle-java7-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections && \
    apt-get install -y oracle-java8-installer && \
    apt-get install -y git && \
    apt-get install -y curl && \
    apt-cache search maven && \
    apt-get install -y maven && \
    apt-get clean
#Configuramos el entorno

ENV JAVA_HOME /usr/lib/jvm/java-8-oracle/
RUN wget http://www.scala-lang.org/files/archive/scala-2.10.4.tgz
RUN mkdir /usr/local/src/scala
RUN tar xvf scala-2.10.4.tgz -C /usr/local/src/scala/
ENV SCALA_HOME /usr/local/src/scala/scala-2.10.4
#RUN echo "export PATH=$SCALA_HOME/bin:$PATH"
RUN wget http://apache.rediris.es/flink/flink-0.10.2/flink-0.10.2-bin-hadoop1.tgz
RUN mkdir /usr/local/src/flink
RUN tar xvf flink-0.10.2-bin-hadoop1.tgz -C /usr/local/src/flink/
ENV FLINK_HOME /usr/local/src/flink/flink-0.10.2
#RUN echo "export PATH=$FLINK_HOME/bin:$PATH"
RUN ln -sf /usr/local/src/flink/flink-0.10.2/bin/ ./flink

RUN rm scala-2.10.4.tgz
RUN rm flink-0.10.2-bin-hadoop1.tgz


ADD init-flink.sh /init-flink.sh
RUN chmod -v +x /init-flink.sh
CMD ["/init-flink.sh"]