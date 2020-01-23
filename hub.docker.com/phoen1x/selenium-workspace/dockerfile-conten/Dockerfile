FROM openjdk:10-jdk

ARG user=jenkins 
ARG group=jenkins 
ARG uid=10000 
ARG gid=10000

ENV HOME /home/${user} 
RUN groupadd -g ${gid} ${group}
RUN useradd -c "Jenkins user" -d $HOME -u ${uid} -g ${gid} -m ${user}
RUN apt-get update \
  && apt-get install -y maven python3 \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ARG VERSION=3.20 
ARG AGENT_WORKDIR=/home/${user}/agent

RUN curl --create-dirs -sSLo /usr/share/jenkins/slave.jar https://repo.jenkins-ci.org/public/org/jenkins-ci/main/remoting/${VERSION}/remoting-${VERSION}.jar \
  && chmod 755 /usr/share/jenkins \
  && chmod 644 /usr/share/jenkins/slave.jar

USER ${user} 
ENV AGENT_WORKDIR=${AGENT_WORKDIR} 
RUN mkdir /home/${user}/.jenkins && mkdir -p ${AGENT_WORKDIR}

VOLUME /home/${user}/.jenkins
VOLUME ${AGENT_WORKDIR}
WORKDIR /home/${user}

COPY jenkins-slave /usr/local/bin/jenkins-slave

ENTRYPOINT ["jenkins-slave"]
