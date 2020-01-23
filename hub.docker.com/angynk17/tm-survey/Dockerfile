FROM tomcat:8.0.43-jre8

ENV ACTIVEMQ_VERSION 5.14.5
ENV ACTIVEMQ apache-activemq-$ACTIVEMQ_VERSION
ENV ACTIVEMQ_TCP=61616 ACTIVEMQ_AMQP=5672 ACTIVEMQ_STOMP=61613 ACTIVEMQ_MQTT=1883 ACTIVEMQ_WS=61614 ACTIVEMQ_UI=8161

ENV ACTIVEMQ_HOME /opt/activemq

RUN set -x && \
    mkdir -p /opt && \
    curl -s -S https://archive.apache.org/dist/activemq/$ACTIVEMQ_VERSION/$ACTIVEMQ-bin.tar.gz | tar xvz -C /opt && \
    ln -s /opt/$ACTIVEMQ $ACTIVEMQ_HOME
	

ADD TMSurveyReportes-1.0.war /usr/local/tomcat/webapps/
ADD TmAPI.war /usr/local/tomcat/webapps/
ADD tomcat-users.xml /usr/local/tomcat/conf/

RUN apt-get update && apt-get install -y supervisor
RUN mkdir -p /var/log/supervisor
RUN mkdir -p /usr/local/temp
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf

EXPOSE 8080
WORKDIR $ACTIVEMQ_HOME
EXPOSE $ACTIVEMQ_TCP $ACTIVEMQ_AMQP $ACTIVEMQ_STOMP $ACTIVEMQ_MQTT $ACTIVEMQ_WS $ACTIVEMQ_UI

CMD chmod 755 $ACTIVEMQ_HOME
CMD chmod 755 /usr/local/temp

CMD ["/usr/bin/supervisord"]


