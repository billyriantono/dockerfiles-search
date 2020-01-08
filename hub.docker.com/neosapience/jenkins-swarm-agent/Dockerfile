FROM docker:18.09.3-dind

ENV SWARM_CLIENT_VERSION=3.15 \
    DOCKER_COMPOSE_VERSION=1.23.2 \
    COMMAND_OPTIONS= \
    USER_NAME_SECRET= \
    PASSWORD_SECRET=

RUN adduser -G root -D jenkins \
 && apk --update --no-cache add openjdk8-jre git openssh py-pip make \
 && wget -q https://repo.jenkins-ci.org/releases/org/jenkins-ci/plugins/swarm-client/${SWARM_CLIENT_VERSION}/swarm-client-${SWARM_CLIENT_VERSION}.jar -P /home/jenkins/ \
 && pip install docker-compose \
 && rm -rf /var/cache/apk/*

COPY run.sh /run.sh
RUN chmod +x /run.sh

CMD ["/run.sh"]