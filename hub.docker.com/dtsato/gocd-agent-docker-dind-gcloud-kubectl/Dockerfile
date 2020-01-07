FROM gocd/gocd-agent-docker-dind:v19.11.0
FROM dtsato/gocd-agent-docker-dind-gcloud:v19.11.0

MAINTAINER Danilo Sato <dtsato@gmail.com>

USER root

ADD https://storage.googleapis.com/kubernetes-release/release/v1.16.3/bin/linux/amd64/kubectl /usr/local/bin/kubectl

RUN chmod +x /usr/local/bin/kubectl

USER go
