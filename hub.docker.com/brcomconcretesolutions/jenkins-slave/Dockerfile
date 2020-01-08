FROM brcomconcretesolutions/jenkins-awscli

ENV JENKINS_SLAVE_AGENT_PORT 50000

USER root

# Configure the nodes
COPY nodes.groovy /usr/share/jenkins/ref/init.groovy.d/nodes.groovy

USER jenkins
