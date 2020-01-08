FROM docker.elastic.co/kibana/kibana:6.1.1
LABEL maintainer "David J. M. Karlsen <david@davidkarlsen.com>"
USER root
RUN yum install -y iproute net-tools
USER kibana
RUN kibana-plugin install https://github.com/sirensolutions/sentinl/releases/download/tag-6.0.0/sentinl-v6.0.0.zip
