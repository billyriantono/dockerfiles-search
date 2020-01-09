FROM jenkins/jenkins:lts

USER root
RUN apt-get update && apt-get install python3 virtualenv -y
RUN cd /opt && \
    wget https://github.com/digitalocean/doctl/releases/download/v1.8.0/doctl-1.8.0-linux-amd64.tar.gz && \
    tar -xf doctl-1.8.0-linux-amd64.tar.gz && \
    chmod a+x doctl && \
    mv doctl /usr/bin/doctl
ENV JENKINS_OPTS -Dorg.jenkinsci.plugins.durabletask.BourneShellScript.HEARTBEAT_CHECK_INTERVAL=600

USER jenkins

