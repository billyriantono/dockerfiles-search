#A Dockerfile for creating a jenkins master image

FROM jenkins

USER root
RUN apt-get update  && apt-get install -y sudo  && rm -rf /var/lib/apt/lists/*
RUN echo "jenkins ALL=NOPASSWD: ALL" >> /etc/sudoers
 
USER jenkins
COPY plugins.txt /usr/share/jenkins/plugins.txt

#add key for github
RUN mkdir /var/jenkins_home/.ssh
USER root
COPY id_rsa /var/jenkins_home/.ssh/id_rsa
RUN chown -R jenkins:jenkins /var/jenkins_home/.ssh/id_rsa
RUN chmod 600 -R /var/jenkins_home/.ssh/id_rsa


USER jenkins
RUN /usr/local/bin/plugins.sh /usr/share/jenkins/plugins.txt
