FROM amazonlinux:2016.09

WORKDIR /root

ENV PATH=$PATH:/root/.local/bin \
    JENKINS_SWARM_VERSION=3.3
ENV JENKINS_SWARM_JAR=swarm-client-$JENKINS_SWARM_VERSION.jar

RUN yum update -y && \
    yum groupinstall -y "Development Tools" && \
    yum install -y java-1.8.0-openjdk-headless jq docker && \
    curl --create-dirs -sSLo /root/${JENKINS_SWARM_JAR} http://repo.jenkins-ci.org/releases/org/jenkins-ci/plugins/swarm-client/${JENKINS_SWARM_VERSION}/${JENKINS_SWARM_JAR} && \
    curl -sL 'https://bootstrap.pypa.io/get-pip.py' | python && \
    pip install virtualenv twine && \
    curl -sL https://raw.githubusercontent.com/mitsuhiko/pipsi/master/get-pipsi.py | python && \
    pipsi install awscli && \
    pipsi install docker-compose==1.11.2 && \
    rm -rf /tmp/* && \
    yum -y clean all

COPY ./start_container.sh /usr/bin/start_container
RUN chmod +x /usr/bin/start_container

CMD ["/usr/bin/start_container"]
