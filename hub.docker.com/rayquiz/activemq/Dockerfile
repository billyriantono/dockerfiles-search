FROM java:7-jre

ENV USR_BASE /usr/local
ENV AMQ_HOME $USR_BASE/apache-activemq
ENV PATH $AMQ_HOME/bin:$PATH
WORKDIR $USR_BASE

RUN curl http://www.mirrorservice.org/sites/ftp.apache.org/activemq/5.12.0/apache-activemq-5.12.0-bin.tar.gz | tar -xz \
	&& ln -s apache-activemq-5.12.0/ apache-activemq

WORKDIR $AMQ_HOME
ADD conf/* conf/

# JMS Tcp connexion
EXPOSE 61616

# Web interface
EXPOSE 8161

VOLUME ["/usr/local/apache-activemq/data"]

CMD ["activemq", "console"]
