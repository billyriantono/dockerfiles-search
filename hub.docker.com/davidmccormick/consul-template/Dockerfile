FROM ubuntu:latest
MAINTAINER David McCormick

ENV CONSUL_TEMPLATE_VERSION 0.18.2

RUN apt-get update && \
    apt-get -y --no-install-recommends install libfontconfig curl ca-certificates && \
    apt-get clean && \
    curl -L -k -O https://releases.hashicorp.com/consul-template/0.18.2/consul-template_0.18.2_linux_amd64.tgz && \
    tar xvfz consul-template_0.18.2_linux_amd64.tgz && \
    mv consul-template /usr/bin/ && \
    rm -rf /consul-template*

ENTRYPOINT [ "consul-template" ]
CMD [ "--help" ]
