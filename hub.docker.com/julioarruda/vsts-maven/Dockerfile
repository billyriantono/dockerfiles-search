FROM ubuntu:16.04

RUN apt update && \
    apt install curl unzip vim apt-transport-https libunwind8 libcurl3 default-jre default-jdk maven sudo -y
RUN curl -sOSL http://security.ubuntu.com/ubuntu/pool/main/i/icu/libicu52_52.1-8ubuntu0.2_amd64.deb && \
    dpkg -i libicu52_52.1-8ubuntu0.2_amd64.deb && \
    rm libicu52_52.1-8ubuntu0.2_amd64.deb
RUN adduser --disabled-password --gecos '' agentuser && \
    adduser agentuser sudo && \
    echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
RUN mkdir /agent
RUN chown -R agentuser:agentuser /agent
USER agentuser
WORKDIR /agent
RUN curl -sOSL https://github.com/Microsoft/vsts-agent/releases/download/v2.102.1/vsts-agent-ubuntu.14.04-x64-2.102.1.tar.gz && \
    tar xzf /agent/vsts-agent-ubuntu.14.04-x64-2.102.1.tar.gz && \
    rm /agent/vsts-agent-ubuntu.14.04-x64-2.102.1.tar.gz
COPY configureAgent.sh runAgent.sh configureAndRun.sh /agent/
USER root
RUN chmod +x configureAndRun.sh configureAgent.sh runAgent.sh && \
    chown agentuser:agentuser configureAgent.sh runAgent.sh configureAndRun.sh
USER agentuser
CMD [ "/agent/configureAndRun.sh" ]
