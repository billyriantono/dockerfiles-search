FROM debian:latest

MAINTAINER Leonardo Amorim de Barros <leoadb@gmail.com>

RUN echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" \
    | tee /etc/apt/sources.list.d/webupd8team-java.list

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys EEA14886

RUN echo "oracle-java8-installer shared/accepted-oracle-license-v1-1 select true" | debconf-set-selections

RUN echo "oracle-java8-installer shared/accepted-oracle-license-v1-1 seen true" | debconf-set-selections

RUN apt-get update && apt-get install -y oracle-java8-installer

RUN cd /tmp && \
    wget http://www.scala-lang.org/files/archive/scala-2.11.8.deb && \
    dpkg -i scala-2.11.8.deb

RUN cd /tmp && \
    wget http://d3kbcqa49mib13.cloudfront.net/spark-2.0.2-bin-hadoop2.7.tgz && \
    tar xvf spark-2.0.2-bin-hadoop2.7.tgz && \
    mv spark-2.0.2-bin-hadoop2.7 /usr/share/spark && \
    rm -rf /tmp/*

ENV SCALA_HOME /usr/share/scala

ENV SPARK_HOME /usr/share/spark

ENV PATH $SPARK_HOME/bin:$PATH

COPY ./run_spark_shell.sh /home

EXPOSE 8080

ENTRYPOINT ["/home/run_spark_shell.sh"]