# Dockerfile
FROM docker:stable
ENV SWARM_CLIENT_VERSION="3.17"

RUN adduser -G root -D jenkins && \
    apk --update --no-cache add openjdk8-jre python python-dev py-pip build-base libffi-dev openssl-dev libgcc git openssh ca-certificates openssl && \
    wget -O swarm-client.jar -q https://repo.jenkins-ci.org/releases/org/jenkins-ci/plugins/swarm-client/${SWARM_CLIENT_VERSION}/swarm-client-${SWARM_CLIENT_VERSION}.jar -P /home/jenkins/ && \
    pip install docker-compose

COPY jenkins-slave.sh /usr/local/bin/jenkins-slave.sh
RUN chmod +x /usr/local/bin/jenkins-slave.sh
CMD ["jenkins-slave.sh"]
