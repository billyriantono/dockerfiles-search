# Use latest jboss/base-jdk:8 image as the base

FROM hwellmann/wildfly-java11:15.0.0.Final

LABEL maintainer="Harald Wellmann <harald.wellmann@gmx.de>"

USER jboss

RUN curl -o /tmp/postgresql-9.4.1212.jar http://repo1.maven.org/maven2/org/postgresql/postgresql/9.4.1212/postgresql-9.4.1212.jar

ADD datasource.cli /tmp/datasource.cli

RUN ${JBOSS_HOME}/bin/jboss-cli.sh --file=/tmp/datasource.cli \
    && rm -rf ${JBOSS_HOME}/standalone/configuration/standalone_xml_history

CMD ["/opt/jboss/wildfly/bin/standalone.sh", "-b", "0.0.0.0"]
