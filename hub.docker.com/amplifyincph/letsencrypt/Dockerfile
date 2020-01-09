FROM ubuntu:16.04 AS installer

RUN apt-get update -y
RUN apt-get install apt-transport-https curl wget gnupg software-properties-common -y
RUN wget -O /tmp/google-apt-key.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg
RUN apt-key add /tmp/google-apt-key.gpg
RUN apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"
RUN apt-get update -y
RUN apt-get install kubectl
RUN wget https://github.com/xenolf/lego/releases/download/v1.2.1/lego_v1.2.1_linux_amd64.tar.gz && \
    tar -xvf lego_v1.2.1_linux_amd64.tar.gz

FROM ubuntu:16.04
RUN apt-get update -y
RUN apt-get install apt-transport-https -y
COPY --from=installer /usr/bin/kubectl /usr/bin/kubectl
COPY --from=installer lego /usr/bin/lego
