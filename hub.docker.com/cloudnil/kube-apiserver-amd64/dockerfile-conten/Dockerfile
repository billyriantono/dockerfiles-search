FROM jenkinsci/jnlp-slave

ARG GO_VERSION=1.9.2

USER root

RUN wget -q https://redirector.gvt1.com/edgedl/go/go${GO_VERSION}.linux-amd64.tar.gz -P /tmp && \
  tar -xf /tmp/go${GO_VERSION}.linux-amd64.tar.gz -C /usr/local

ENV PATH=/usr/local/go/bin:$PATH

VOLUME artifacts

USER jenkins

ENTRYPOINT ["/usr/local/bin/jenkins-slave"]
