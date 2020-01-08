FROM jenkins
MAINTAINER Samuel Seidel

# Prep Jenkins Directories
USER root
RUN mkdir /var/log/jenkins
RUN mkdir /var/cache/jenkins
RUN chown -R jenkins:jenkins /var/log/jenkins
RUN chown -R jenkins:jenkins /var/cache/jenkins
USER jenkins

# Set Defaults
ENV TZ=America/New_York
ENV JAVA_OPTS="-Xmx8192m"
ENV JENKINS_JAVA_OPTIONS="-Duser.timezone=America/New_York"
ENV JENKINS_OPTS="--handlerCountMax=300 --logfile=/var/log/jenkins/jenkins.log  --webroot=/var/cache/jenkins/war"
