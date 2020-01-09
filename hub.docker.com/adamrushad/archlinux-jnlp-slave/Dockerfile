FROM archlinux:latest
MAINTAINER AdamRushad <2429990+adamrushad@users.noreply.github.com>

#Install
RUN pacman -Syu --noconfirm && pacman -S jre8-openjdk-headless --noconfirm && pacman -Scc --noconfirm

#Workspace volume
VOLUME ["/workspace"]

# Entrypoint
COPY ./jenkins-slave /usr/local/bin/jenkins-slave
ENTRYPOINT ["/usr/local/bin/jenkins-slave"]

ARG BUILD_DATE
ARG VCS_REF
ARG VERSION
LABEL org.label-schema.build-date=$BUILD_DATE \
  org.label-schema.name="Basic ArchLinux Jenkins Slave" \
  org.label-schema.description="Barebones ArchLinux Jenkins JNLP Slave" \
  org.label-schema.url="https://github.com/adamrushad/archlinux-jnlp-slave/" \
  org.label-schema.vcs-ref=$VCS_REF \
  org.label-schema.vcs-url="https://github.com/adamrushad/archlinux-jnlp-slave" \
  org.label-schema.version=$VERSION \
  org.label-schema.schema-version="1.0"
