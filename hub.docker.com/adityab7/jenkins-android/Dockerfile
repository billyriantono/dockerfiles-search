FROM openjdk:8-jdk-stretch

RUN apt-get update && apt-get upgrade -y && \
    apt-get install -y autoconf automake axel bc bison build-essential clang cmake expat flex g++ g++-multilib gawk gcc gcc-multilib \
        gnupg gperf htop imagemagick lib32ncurses5-dev lib32z1-dev libtinfo5 libc6-dev libcap-dev libexpat1-dev \
        libgmp-dev liblz4-* liblzma* libmpc-dev libmpfr-dev libncurses5-dev libsdl1.2-dev libssl-dev libtool libxml2 \
        libxml2-utils lzma* lzop maven ncftp ncurses-dev patch patchelf pkg-config pngcrush pngquant python python-all-dev \
        re2c schedtool squashfs-tools subversion texinfo unzip w3m xsltproc zip zlib1g-dev curl git sudo rsync && \
    rm -rf /var/lib/apt/lists/*

# Install repo binary (thanks to Akhil Narang)
RUN curl --create-dirs -L -o /usr/local/bin/repo -O -L https://github.com/akhilnarang/repo/raw/master/repo && \
    chmod a+x /usr/local/bin/repo

ARG user=jenkins
ARG group=jenkins
ARG uid=1000
ARG gid=1000
ARG http_port=8080
ARG agent_port=50000
ARG JENKINS_HOME=/var/jenkins_home

ENV JENKINS_HOME $JENKINS_HOME
ENV JENKINS_SLAVE_AGENT_PORT ${agent_port}
ENV USE_CCACHE=1 \
    CCACHE_DIR=/tmp/ccache

# Jenkins is run with user `jenkins`, uid = 1000
# If you bind mount a volume from the host or a data container,
# ensure you use the same uid
RUN mkdir -p $JENKINS_HOME && \
  chown ${uid}:${gid} $JENKINS_HOME && \
  groupadd -g ${gid} ${group} && \
  useradd -d "$JENKINS_HOME" -u ${uid} -g ${gid} -m -s /bin/bash ${user} && \
  mkdir -p /tmp/ccache && \
  chown -R ${user}: /tmp/ccache

# Allow sudo without password for build user
RUN echo "${user} ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/90-docker-build && \
  usermod -aG sudo ${user}
    
# Jenkins home directory is a volume, so configuration and build history
# can be persisted and survive image upgrades
VOLUME ["/tmp/ccache", "$JENKINS_HOME"]

# `/usr/share/jenkins/ref/` contains all reference configuration we want
# to set on a fresh new installation. Use it to bundle additional plugins
# or config file with your custom jenkins Docker image.
RUN mkdir -p /usr/share/jenkins/ref/init.groovy.d

# Use tini as subreaper in Docker container to adopt zombie processes
ARG TINI_VERSION=v0.16.1
COPY tini_pub.gpg ${JENKINS_HOME}/tini_pub.gpg
RUN curl -fsSL https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini-static-$(dpkg --print-architecture) -o /sbin/tini \
  && curl -fsSL https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini-static-$(dpkg --print-architecture).asc -o /sbin/tini.asc \
  && gpg --no-tty --import ${JENKINS_HOME}/tini_pub.gpg \
  && gpg --verify /sbin/tini.asc \
  && rm -rf /sbin/tini.asc /root/.gnupg \
  && chmod +x /sbin/tini

# jenkins version being bundled in this docker image
ARG JENKINS_VERSION
ENV JENKINS_VERSION ${JENKINS_VERSION:-2.184}

# jenkins.war checksum, download will be validated using it
ARG JENKINS_SHA=ca99d046d34b58d6a6276cc8337e04cb61aedd7818f5142b480072905a05c4c9

# Can be used to customize where jenkins.war get downloaded from
ARG JENKINS_URL=https://repo.jenkins-ci.org/public/org/jenkins-ci/main/jenkins-war/${JENKINS_VERSION}/jenkins-war-${JENKINS_VERSION}.war

# could use ADD but this one does not check Last-Modified header neither does it allow to control checksum
# see https://github.com/docker/docker/issues/8331
RUN curl -fsSL ${JENKINS_URL} -o /usr/share/jenkins/jenkins.war \
  && echo "${JENKINS_SHA}  /usr/share/jenkins/jenkins.war" | sha256sum -c -

ENV JENKINS_UC https://updates.jenkins.io
ENV JENKINS_UC_EXPERIMENTAL=https://updates.jenkins.io/experimental
ENV JENKINS_INCREMENTALS_REPO_MIRROR=https://repo.jenkins-ci.org/incrementals
RUN chown -R ${user} "$JENKINS_HOME" /usr/share/jenkins/ref

# for main web interface:
EXPOSE ${http_port}

# will be used by attached slave agents:
EXPOSE ${agent_port}

ENV COPY_REFERENCE_FILE_LOG $JENKINS_HOME/copy_reference_file.log

USER ${user}

# Create gitconfig for build user
RUN git config --global user.name "Aditya" && git config --global user.email "adityab7@protonmail.com" && \
    git config --global color.ui auto

COPY jenkins-support /usr/local/bin/jenkins-support
COPY jenkins.sh /usr/local/bin/jenkins.sh
COPY tini-shim.sh /bin/tini
ENTRYPOINT ["/sbin/tini", "--", "/usr/local/bin/jenkins.sh"]

# from a derived Dockerfile, can use `RUN plugins.sh active.txt` to setup /usr/share/jenkins/ref/plugins from a support bundle
COPY plugins.sh /usr/local/bin/plugins.sh
COPY install-plugins.sh /usr/local/bin/install-plugins.sh
