FROM jenkins/jenkins:2.182


# Install plugins defined in plugins.txt
COPY plugins.txt /var/jenkins_home/plugins.txt
RUN /usr/local/bin/install-plugins.sh < /var/jenkins_home/plugins.txt


USER jenkins
