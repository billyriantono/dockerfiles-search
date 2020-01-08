FROM ubuntu:bionic
RUN apt-get update && apt-get -y install openjdk-8-jdk-headless maven
ADD buildagent /opt/buildagent
CMD /opt/buildagent/bin/agent.sh console
