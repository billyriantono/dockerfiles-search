FROM rastasheep/ubuntu-sshd:14.04

ENV JBOSS_VERSION 7.1
ENV JBOSS_FULL_VERSION $JBOSS_VERSION.1.Final
ENV JBOSS_HOME /opt/jboss

RUN apt-get update && apt-get install -y curl openjdk-7-jre-headless --no-install-recommends



RUN cd /opt && curl http://download.jboss.org/jbossas/$JBOSS_VERSION/jboss-as-$JBOSS_FULL_VERSION/jboss-as-$JBOSS_FULL_VERSION.tar.gz | tar zx && mv /opt/jboss-as-$JBOSS_FULL_VERSION /opt/jboss

# RUN cd $JBOSS_HOME/standalone/configuration/ && \
#    sed -i 's/enable-welcome-root="true"/enable-welcome-root="false"/g' standalone.xml && \
#    sed -i 's/127.0.0.1/0.0.0.0/g' standalone.xml && \
#    sed -i 's/<deployment-scanner/<deployment-scanner auto-deploy-exploded="true"/g' standalone.xml

EXPOSE 8081

CMD /usr/sbin/sshd && /opt/jboss/bin/standalone.sh -b 0.0.0.0 -Djboss.http.port=8081
