FROM hashicorp/packer:1.5.1 as builder

FROM gocd/gocd-agent-centos-7:v19.12.0

USER root
RUN yum install -y \
    git \
    bash \
    openssl \
    && yum clean all
COPY --from=builder /bin/packer /usr/local/bin/packer

USER go