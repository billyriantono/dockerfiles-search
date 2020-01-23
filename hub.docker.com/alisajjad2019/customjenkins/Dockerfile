ARG JENKINS_HOME=/var/jenkins_home
FROM jenkins/jenkins:lts
RUN whoami
USER root
RUN whoami
RUN chown -R jenkins:jenkins ${JENKINS_HOME}
COPY jenkins_home ${JENKINS_HOME}
 