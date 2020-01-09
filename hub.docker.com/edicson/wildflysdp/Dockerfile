FROM jboss/wildfly:10.1.0.Final

CMD ["echo","Creating Entsia Wildfly Docker Image with configurations for SDP !!!"]

ENV BOOMER_DB_NAME calliden_boomer
ENV BOOMER_USER_NAME boomer_runtime
ENV BOOMER_USER_PASSWORD p@55w0rd!!
ENV BOOMER_DEFAULT_SCHEMA calliden_boomer

ENV HELO_DB_NAME calliden_helo
ENV HELO_USER_NAME helo_runtime
ENV HELO_USER_PASSWORD p@55w0rd!!
ENV HELO_DEFAULT_SCHEMA calliden_helo

COPY config/WildFly.sh $HOME
COPY config/WildFlyConfiguration.cli $HOME
COPY modules/com.zip $JBOSS_HOME/modules
COPY modules/org.zip $JBOSS_HOME/modules

#To extract hsqldb,oracle and sqlserver modules
RUN \
    cd $JBOSS_HOME/modules && \
    unzip com.zip && \
    unzip org.zip

RUN rm $JBOSS_HOME/modules/*.zip

#To create all the sdp-wildfly configuration using cli
RUN /bin/sh -c '$JBOSS_HOME/bin/standalone.sh --server-config=standalone-full.xml &' && \
  sleep 60 && \
  $HOME/WildFly.sh

RUN /opt/jboss/wildfly/bin/add-user.sh entsia Entsia2017! --silent

#To expose admin port
EXPOSE 9990

CMD ["echo","Finishing configuration, Entsia Wildfly Docker Image with configurations for SDP  is ready to use!!!"]

# Define default command that will be executed when the container starts.
CMD ["/opt/jboss/wildfly/bin/standalone.sh", "-b", "0.0.0.0", "-bmanagement", "0.0.0.0", "-c", "standalone-full.xml"]
