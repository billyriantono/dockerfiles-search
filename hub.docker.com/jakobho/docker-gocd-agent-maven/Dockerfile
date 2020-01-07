FROM maven:3.5.3-jdk-8-slim

RUN apt-get update
RUN apt-get install -y apt-transport-https
RUN apt-get install -y gnupg
RUN apt-get install -y git

RUN echo "deb https://download.gocd.org /" | tee /etc/apt/sources.list.d/gocd.list
RUN curl https://download.gocd.org/GOCD-GPG-KEY.asc | apt-key add -
RUN apt-get update
RUN apt-get install -y go-agent

ENTRYPOINT ["/bin/bash", "/usr/share/go-agent/agent.sh"]
