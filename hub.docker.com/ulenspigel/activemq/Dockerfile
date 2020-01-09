FROM alpine:latest
RUN apk add --no-cache openjdk8-jre
ENV JAVA_HOME=/usr
ENV PATH=$PATH:$JAVA_HOME
ENV ACTIVEMQ_NAME=apache-activemq-5.15.7
ENV ACTIVEMQ_FILE=$ACTIVEMQ_NAME-bin.tar.gz
WORKDIR /home
RUN apk add --no-cache wget && \
	wget -O $ACTIVEMQ_FILE "http://www.apache.org/dyn/closer.cgi?filename=/activemq/5.15.7/apache-activemq-5.15.7-bin.tar.gz&action=download" && \
    tar -xzf $ACTIVEMQ_FILE -C /home/ && \
    rm /home/$ACTIVEMQ_FILE && \
	apk del wget
EXPOSE 8161 61616
ENTRYPOINT /home/$ACTIVEMQ_NAME/bin/activemq start && tail -f /dev/null
CMD ["/bin/sh"]
