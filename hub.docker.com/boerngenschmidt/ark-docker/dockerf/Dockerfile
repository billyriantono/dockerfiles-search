FROM openjdk:8-jdk-alpine

ENV JENKINS_HOME=/opt/jenkins

COPY entrypoint.sh /usr/local/bin/entrypoint.sh

RUN set -x && \
    apk add --no-cache bash docker expect git openssh-client ttf-dejavu wget && \
    mkdir -p /opt/jenkins && \
    wget -q -O /opt/jenkins.war http://mirrors.jenkins.io/war-stable/latest/jenkins.war && \
    git config --system http.sslVerify false

EXPOSE 8080 50000

ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
