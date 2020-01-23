FROM jolokia/java-jolokia:7

MAINTAINER deppisch@consol.de

EXPOSE 61616 8161 61613 1883 61614 5672

ENV ACTIVEMQ_VERSION 5.11.2

# Get and Unpack
RUN curl --output /tmp/apache-activemq.zip http://central.maven.org/maven2/org/apache/activemq/apache-activemq/${ACTIVEMQ_VERSION}/apache-activemq-${ACTIVEMQ_VERSION}-bin.zip
RUN cd /opt && unzip /tmp/apache-activemq.zip
RUN ln -s /opt/apache-activemq-${ACTIVEMQ_VERSION} /opt/apache-activemq
RUN chmod a+x /opt/apache-activemq/bin/activemq

# Add config
ADD conf /opt/apache-activemq/conf

# Remove unneeded files
RUN rm /tmp/apache-activemq.zip
RUN rm -rf /opt/apache-activemq/examples
RUN rm -rf /opt/apache-activemq/docs
RUN rm -rf /opt/apache-activemq/webapps-demo

VOLUME ["/opt/apache-activemq/data"]

ENV ACTIVEMQ_HOME /opt/apache-activemq
ENV PATH $PATH:$ACTIVEMQ_HOME/bin

CMD /opt/apache-activemq/bin/activemq console
