FROM jackboot7/jboss7
MAINTAINER isidromerayo isidro.merayo@gmail.com

# language
ENV LC_ALL en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US.UTF-8
ENV JBOSS_HOME /opt/jboss

#
# JBoss Custom
#

# Oracle Driver
RUN  mkdir -p $JBOSS_HOME/modules/system/layers/base/com/oracle/main/
COPY JDBC/ojdbc6.jar $JBOSS_HOME/modules/system/layers/base/com/oracle/main/
COPY JDBC/module.xml $JBOSS_HOME/modules/system/layers/base/com/oracle/main/

# custom configuration with Oracle Driver
COPY standalone.xml $JBOSS_HOME/standalone/configuration/

# Dummy project
ADD ModuleEAR.ear $JBOSS_HOME/standalone/deployments/
USER root
RUN chown jboss:jboss $JBOSS_HOME/standalone/deployments/ModuleEAR.ear
USER jboss
