FROM java:openjdk-8u77-jdk-alpine

RUN wget -O /root/jenkins.war http://mirrors.jenkins-ci.org/war/1.656/jenkins.war
RUN chmod 644 /root/jenkins.war
ENV JENKINS_HOME /root/jenkins

RUN apk add --no-cache openssh-client fontconfig ttf-dejavu
RUN apk add --update --repository http://dl-cdn.alpinelinux.org/alpine/edge/community/ tini

VOLUME ["/root/jenkins"]

ENTRYPOINT ["/usr/bin/tini", "--"]
CMD ["java", "-jar", "-Djava.awt.headless=true", "/root/jenkins.war"]
EXPOSE 8080
