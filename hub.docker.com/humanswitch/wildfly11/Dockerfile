FROM jboss/wildfly:11.0.0.Final

ENV JBOSS_HOME /opt/jboss/wildfly
ADD jboss-cli-docker.sh $JBOSS_HOME/bin

USER root

RUN chmod ug+x $JBOSS_HOME/bin/jboss-cli-docker.sh \
    && sed -i "s/<resolve-parameter-values>false<\/resolve-parameter-values>/ \
        <resolve-parameter-values>true<\/resolve-parameter-values>/" \
        $JBOSS_HOME/bin/jboss-cli.xml

USER jboss