FROM ubuntu:12.04
MAINTAINER Allan Espinosa "allan.espinosa@outlook.com"

RUN echo deb http://archive.ubuntu.com/ubuntu precise universe >> /etc/apt/sources.list
RUN apt-get update && apt-get clean
RUN apt-get install -q -y openjdk-7-jre-headless && apt-get clean
ADD http://mirrors.jenkins-ci.org/war/1.562/jenkins.war /opt/jenkins.war
RUN chmod 644 /opt/jenkins.war
RUN adduser --system jenkins --group --home /var/lib/jenkins --disabled-login --disabled-password
RUN ln -sf /jenkins /var/lib/jenkins

ENV JENKINS_HOME /var/lib/jenkins
USER jenkins
ENTRYPOINT ["java", "-jar", "/opt/jenkins.war"]
EXPOSE 8080
VOLUME ["/jenkins"]
CMD [""]
