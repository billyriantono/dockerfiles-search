FROM jenkins/jenkins:lts
USER root

# Add docker repo
RUN apt-get update && \
    apt-get install -y --no-install-recommends software-properties-common \
        ca-certificates \
        curl \
        apt-transport-https \
        gnupg2 \
        rsync \
        build-essential && \
    rm -rf /var/lib/apt/lists/*

RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -
RUN add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian stretch stable"

RUN usermod -u 504 jenkins

RUN chown -R jenkins:jenkins /var/jenkins_home
RUN rm /etc/localtime && ln -s /usr/share/zoneinfo/Europe/Stockholm /etc/localtime
ENV JENKINS_OPTS $JENKINS_OPTS -Dorg.apache.commons.jelly.tags.fmt.timeZone=Europe/Stockholm

RUN apt-get update && \
    apt-get install -y docker-ce && \
    rm -rf /var/lib/apt/lists/*

# Remember that the local docker group needs to have the same GID as the owning group of /var/run/docker.socket
# Horrible hack to set docker GID to same as host GID
RUN groupmod -g 502 docker
RUN usermod -a -G docker jenkins

USER jenkins
ARG BUILD_DATE
ARG VCS_REF
ARG VERSION
LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="https://bitbucket.org/unikumdev/buildscripts" \
      org.label-schema.vendor="Unikum Unikt Lärande AB" \
      org.label-schema.version=$VERSION \
      org.label-schema.schema-version="1.0"

