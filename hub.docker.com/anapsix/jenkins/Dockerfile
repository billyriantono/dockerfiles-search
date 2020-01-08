FROM anapsix/alpine-java:jre8
MAINTAINER Anastas Dancha "anapsix@random.io"
ENV JENKINS_HOME /opt/jenkins
ADD http://mirrors.jenkins-ci.org/war/latest/jenkins.war /srv/jenkins.war
VOLUME /opt/jenkins
EXPOSE 8080/tcp 22/tcp
WORKDIR /tmp
CMD ["java","-jar","/srv/jenkins.war"]
