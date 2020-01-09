FROM jboss/wildfly:14.0.0.Final

USER root

# RUN yum update -y

RUN ln -s $JBOSS_HOME/standalone/deployments /deployments
RUN /opt/jboss/wildfly/bin/add-user.sh admin test --silent

VOLUME /deployments

EXPOSE 9990

CMD ["/opt/jboss/wildfly/bin/standalone.sh", "--server-config" ,"standalone-full.xml", "-b", "0.0.0.0", "-bmanagement", "0.0.0.0"]

