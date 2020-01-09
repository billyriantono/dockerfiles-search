FROM jboss/wildfly:9.0.1.Final

#As root to change the permissions of the module to the user jboss.
USER root
ADD http://repo.maven.apache.org/maven2/io/dropwizard/metrics/metrics-core/3.1.2/metrics-core-3.1.2.jar /opt/jboss/wildfly/modules/system/layers/base/io/dropwizard/metrics/core/main/
COPY modules /opt/jboss/wildfly/modules/system/layers/base/
RUN chown -R jboss:jboss /opt/jboss/wildfly/modules/system/layers/base/io/dropwizard/metrics
USER jboss

#copy the war of example to the deployments of the WildFly
COPY metrics-0.0.1-SNAPSHOT.war /opt/jboss/wildfly/standalone/deployments/metrics.war

#An admin user
RUN /opt/jboss/wildfly/bin/add-user.sh admin Admin#70365 --silent

#expose the admin port
EXPOSE 9990

CMD ["/opt/jboss/wildfly/bin/standalone.sh", "-b", "0.0.0.0", "-bmanagement", "0.0.0.0"]
