FROM python:3.7-stretch

MAINTAINER  Ludwig Prager <ludwig.prager@celp.de>

RUN apt-get update && apt-get -y install \
	wget \
        net-tools \
        supervisor \
	vim less  \
default-jdk

# software-properties-common  && \
#add-apt-repository "deb http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" && \
#apt update && \
#apt-get install oracle-java8-installer


RUN rm -rf /var/lib/apt/lists/*

#COPY supervisord.conf /etc/supervisor/supervisord.conf


ENV HADOOP 2.7
ENV SPARK 2.4.4

ENV SPARK_ARCHIVE spark-${SPARK}-bin-hadoop${HADOOP}.tgz
RUN wget https://archive.apache.org/dist/spark/spark-${SPARK}/spark-${SPARK}-bin-hadoop${HADOOP}.tgz
RUN tar -zxf ${SPARK_ARCHIVE}
RUN rm ${SPARK_ARCHIVE}

RUN echo "SPARK_HOME=/spark-${SPARK}-bin-hadoop${HADOOP}/" >> ~/.bashrc
RUN echo 'PATH=$PATH:/spark-'${SPARK}'-bin-hadoop${HADOOP}/sbin' >> ~/.bashrc
RUN echo 'PATH=$PATH:/spark-'${SPARK}'-bin-hadoop${HADOOP}/bin' >> ~/.bashrc

ADD cmd.sh /bin/
RUN chmod +x /bin/cmd.sh

WORKDIR /my_project/

#CMD ["/spark-2.4.4-bin-hadoop2.7/sbin/start-master.sh"]
#RUN ["/bin/bash"]
#RUN ["/bin/bash"]

CMD bash /bin/cmd.sh
