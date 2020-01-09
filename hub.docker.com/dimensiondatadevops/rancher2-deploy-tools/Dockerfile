FROM centos:centos7

ADD kubernetes.repo /etc/yum.repos.d/

RUN yum update -y
RUN yum install -y kubectl

ENV RKE_LATEST_VERSION="v0.1.13"

RUN curl -L https://github.com/rancher/rke/releases/download/${RKE_LATEST_VERSION}/rke_linux-amd64 -o /usr/bin/rke_linux-amd64 \
&& chmod +x /usr/bin/rke_linux-amd64 \
&& mv /usr/bin/rke_linux-amd64 /usr/bin/rke

ENV HELM_LATEST_VERSION="v2.12.0"

RUN curl -L https://storage.googleapis.com/kubernetes-helm/helm-${HELM_LATEST_VERSION}-linux-amd64.tar.gz -o ~/helm-linux-amd64.tar.gz \
&& cd ~/ \
&& tar xzf helm-linux-amd64.tar.gz \
&& cp ~/linux-amd64/helm /usr/bin/helm \
&& cp ~/linux-amd64/tiller /usr/bin/tiller \
&& rm -rf ~/linux-amd64 \
&& rm -rf ~/helm-linux-amd64.tar.gz

RUN mkdir /working
WORKDIR /working
ENTRYPOINT [ "/bin/sh" ]

