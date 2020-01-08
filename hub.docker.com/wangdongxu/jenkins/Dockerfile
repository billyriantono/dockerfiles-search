FROM wangdongxu/java:jdk8
ADD http://mirrors.jenkins-ci.org/war/2.102/jenkins.war /opt/jenkins.war
RUN chmod 644 /opt/jenkins.war
ENV JENKINS_HOME /jenkins
ADD https://download.docker.com/linux/static/stable/x86_64/docker-17.09.0-ce.tgz /tmp/docker.tgz
RUN cd /tmp \
    && tar -zxvf docker.tgz \
    && mv docker/docker* /bin/ \
    && rm -rf docker
ENTRYPOINT ["java", "-jar", "/opt/jenkins.war" ,"-Djava.awt.headless=true"]
EXPOSE 8080
