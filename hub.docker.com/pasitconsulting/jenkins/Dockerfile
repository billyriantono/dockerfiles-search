FROM ubuntu:16.04
LABEL maintainer="pasitconsulting@outlook.com"
RUN apt update
RUN apt-get -y install default-jre wget sudo gnupg vim
RUN wget -q -O - https://pkg.jenkins.io/debian/jenkins-ci.org.key | sudo apt-key add -
RUN sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
RUN apt update
WORKDIR /var/lib/jenkins
RUN apt-get install -y jenkins
ADD --chown=jenkins:jenkins config.xml config.xml
ADD --chown=jenkins:jenkins plugins plugins/
#RUN mkdir /var/run/jenkins
CMD service jenkins start && tail -F /var/log/jenkins/jenkins.log
