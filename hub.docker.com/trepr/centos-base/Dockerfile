FROM centos:7
LABEL maintainer="TRE-PR/SECTI/COSIS/Seção de Desenvolvimento de Sistemas <sds@tre-pr.jus.br>" \
      description="Imagem docker base centos"

USER root

# Add TRE-PR CA root certificate and update trusted
COPY --chown=root:root tre-root-v2.crt /etc/pki/ca-trust/source/anchors/tre-root-v2.crt

# Install base packages, configure certs
RUN yum update -y \
    && yum -y install \
        xmlstarlet saxon augeas bsdtar unzip \
    && yum clean all \
    && update-ca-trust extract
