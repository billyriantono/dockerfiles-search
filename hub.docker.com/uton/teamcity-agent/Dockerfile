FROM jetbrains/teamcity-agent:2018.1.2

ENV DOCKER_VERSION 17.12.1
ENV KUBECTL_VERSION 1.6.4
ENV HOME=/config

RUN apt-get update

RUN apt-get install docker-ce=${DOCKER_VERSION}~ce-0~ubuntu -y --allow-downgrades
RUN apt-cache policy docker-ce
RUN apt-get install jq -y

ADD https://storage.googleapis.com/kubernetes-release/release/v${KUBECTL_VERSION}/bin/linux/amd64/kubectl /usr/local/bin/kubectl
RUN chmod +x /usr/local/bin/kubectl
