FROM jenkins:1.625.3

USER root

RUN apt-get update && apt-get install -y ca-certificates libapparmor-dev
ADD ./run.sh /run.sh

ENV SWARM_CLIENT_VERSION 2.0

ADD http://repo.jenkins-ci.org/releases/org/jenkins-ci/plugins/swarm-client/${SWARM_CLIENT_VERSION}/swarm-client-${SWARM_CLIENT_VERSION}-jar-with-dependencies.jar \
  /usr/share/jenkins/swarm-client-${SWARM_CLIENT_VERSION}.jar

RUN chmod 644 /usr/share/jenkins/swarm-client-${SWARM_CLIENT_VERSION}.jar

RUN curl -fsSLO https://get.docker.com/builds/Linux/x86_64/docker-17.05.0-ce.tgz \
  && tar --strip-components=1 -xvzf docker-17.05.0-ce.tgz -C /usr/local/bin \
  && chmod +x /usr/local/bin/docker \
  && rm docker-17.05.0-ce.tgz

RUN curl -L https://github.com/docker/compose/releases/download/1.13.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose \
  && chmod +x /usr/local/bin/docker-compose


USER jenkins
WORKDIR /var/jenkins_home

ENTRYPOINT ["/run.sh"]
