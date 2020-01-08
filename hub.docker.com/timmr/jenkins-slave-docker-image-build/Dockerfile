FROM jenkinsci/jnlp-slave:2.52

USER root

# minikube
RUN groupadd --gid 1001 docker
RUN adduser jenkins docker

RUN curl -o /tmp/helm.tar.gz https://storage.googleapis.com/kubernetes-helm/helm-v2.4.2-linux-amd64.tar.gz \
  && cd /tmp/ \
  && tar xzf helm.tar.gz \
  && cp linux-amd64/helm /usr/local/bin/

RUN curl -o /usr/local/bin/kubectl https://storage.googleapis.com/kubernetes-release/release/v1.6.4/bin/linux/amd64/kubectl && chmod 755 /usr/local/bin/kubectl

USER jenkins
