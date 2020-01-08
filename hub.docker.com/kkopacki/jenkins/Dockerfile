FROM java:openjdk-7u75-jdk
MAINTAINER kkopacki

RUN apt-get update && apt-get clean
ADD http://mirrors.jenkins-ci.org/war/1.605/jenkins.war /usr/share/jenkins/jenkins.war
RUN chmod 644 /usr/share/jenkins/jenkins.war

ENV JENKINS_HOME /var/lib/jenkins

ENTRYPOINT ["java", "-jar", "/usr/share/jenkins/jenkins.war"]
EXPOSE 8080
CMD [""]
