FROM jeanblanchard/busybox-java
MAINTAINER Jahroots "Jahroots@gmail.com"

ADD http://mirrors.jenkins-ci.org/war/latest/jenkins.war /opt/jenkins.war
RUN ln -sf /jenkins /root/.jenkins

EXPOSE 8080
VOLUME ["/jenkins"]
ENTRYPOINT ["java", "-jar", "/opt/jenkins.war"]