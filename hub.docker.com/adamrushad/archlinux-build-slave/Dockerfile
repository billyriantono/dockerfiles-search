FROM adamrushad/archlinux-jnlp-slave:latest
MAINTAINER AdamRushad <2429990+adamrushad@users.noreply.github.com>

ARG user=jenkins
ARG group=jenkins
ARG uid=975
ARG gid=975

#Install
RUN groupadd -g ${gid} ${group} && useradd -c "Jenkins user" -d /home/${user} -u ${uid} -g ${gid} -m ${user}
RUN touch /agent.log && chown ${user}:${group} /agent.log && chown -R ${user}:${group} /workspace
RUN pacman -Syu --noconfirm && pacman -S base-devel git --noconfirm && pacman -Scc --noconfirm 

USER ${user}:${group}

COPY jenkins.sudoers /etc/sudoers.d/jenkins

ARG BUILD_DATE
ARG VCS_REF
ARG VERSION
LABEL org.label-schema.build-date=$BUILD_DATE \
  org.label-schema.name="ArchLinux Package Builder Jenkins Slave" \
  org.label-schema.description="ArchLinux Jenkins JNLP Slave for building ArchLinux packages" \
  org.label-schema.url="https://github.com/adamrushad/archlinux-build-slave/" \
  org.label-schema.vcs-ref=$VCS_REF \
  org.label-schema.vcs-url="https://github.com/adamrushad/archlinux-build-slave" \
  org.label-schema.version=$VERSION \
  org.label-schema.schema-version="1.0"
