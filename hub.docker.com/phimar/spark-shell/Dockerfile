FROM centos:6

RUN yum -y install tar

RUN curl -LO 'http://download.oracle.com/otn-pub/java/jdk/7u71-b14/jdk-7u71-linux-x64.rpm' -H 'Cookie: oraclelicense=accept-securebackup-cookie'
RUN rpm -i jdk-7u71-linux-x64.rpm
RUN rm jdk-7u71-linux-x64.rpm

ENV JAVA_HOME /usr/java/default
ENV PATH $PATH:$JAVA_HOME/bin

RUN curl -s http://apache.openmirror.de/spark/spark-1.5.1/spark-1.5.1-bin-hadoop2.6.tgz | tar zx -C /usr/local/
RUN cd /usr/local && ln -s spark-1.5.1-bin-hadoop2.6 spark
ENV SPARK_HOME /usr/local/spark

CMD /usr/local/spark/bin/spark-shell --master spark://$MASTER_PORT_7077_TCP_ADDR:$MASTER_PORT_7077_TCP_PORT