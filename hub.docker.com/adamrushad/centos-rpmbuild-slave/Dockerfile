FROM adamrushad/centos-jnlp-slave:8
MAINTAINER AdamRushad <2429990+adamrushad@users.noreply.github.com>

#Install
RUN dnf -y install epel-release && dnf -y install mock rpm-build && dnf clean all

ARG BUILD_DATE
ARG VCS_REF
ARG VERSION
LABEL org.label-schema.build-date=$BUILD_DATE \
  org.label-schema.name="CentOS RPMBuild Jenkins Slave" \
  org.label-schema.description="CentOS Jenkins JNLP Slave for building RPMs" \
  org.label-schema.url="https://github.com/adamrushad/centos-rpmbuild-slave/" \
  org.label-schema.vcs-ref=$VCS_REF \
  org.label-schema.vcs-url="https://github.com/adamrushad/centos-rpmbuild-slave" \
  org.label-schema.version=$VERSION \
  org.label-schema.schema-version="1.0"
