FROM debian:10-slim

RUN export KUBE_VERSION="v1.16.2"
RUN export DOCTL_VERSION="1.33.1"
RUN export TERRAFORM_VERSION="0.12.12"

RUN apt update

RUN apt install -y ca-certificates curl gettext jq wget unzip

RUN wget -O /doctl.tar.gz "https://github.com/digitalocean/doctl/releases/download/v1.33.1/doctl-1.33.1-linux-amd64.tar.gz" && tar xvzf /doctl.tar.gz -C /bin

#RUN ln -s /lib/libc.musl-x86_64.so.1 /lib64/ld-linux-x86-64.so.2

RUN curl -L https://storage.googleapis.com/kubernetes-release/release/v1.16.2/bin/linux/amd64/kubectl -o /usr/local/bin/kubectl \
    && chmod +x /usr/local/bin/kubectl

RUN wget -q -O /terraform.zip "https://releases.hashicorp.com/terraform/0.12.12/terraform_0.12.12_linux_amd64.zip" \
    && unzip /terraform.zip -d /bin \
    && rm -f /terraform.zip

RUN apt update
RUN apt-get install -y apt-transport-https gnupg-agent software-properties-common

RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -
RUN apt-key fingerprint 0EBFCD88
RUN add-apt-repository \
       "deb [arch=amd64] https://download.docker.com/linux/debian \
       $(lsb_release -cs) \
       stable"
RUN apt update
RUN apt-get install -y docker-ce docker-ce-cli containerd.io

