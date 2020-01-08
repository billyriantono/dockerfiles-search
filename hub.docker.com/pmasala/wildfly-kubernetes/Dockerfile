FROM jboss/wildfly:15.0.1.Final

LABEL MAINTAINER Pietrangelo Masala <pietrangelo.masala@gmail.com>

USER root

COPY ssh-scripts/docker-entrypoint.sh $JBOSS_HOME/docker-entrypoint.sh
RUN chown jboss $JBOSS_HOME/docker-entrypoint.sh && \
 	chmod a+x $JBOSS_HOME/docker-entrypoint.sh

COPY standalone-ha.xml $JBOSS_HOME/standalone/configuration/
COPY standalone-full-ha.xml $JBOSS_HOME/standalone/configuration/


EXPOSE 8080 8009 9990 7600 8888

ENTRYPOINT $JBOSS_HOME/docker-entrypoint.sh
