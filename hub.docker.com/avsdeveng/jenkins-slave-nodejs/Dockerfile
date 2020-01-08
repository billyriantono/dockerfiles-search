FROM centos:centos7
MAINTAINER "Nick Griffin" <nicholas.griffin@accenture.com>

# Java Env Variables
ENV JAVA_VERSION=1.8.0_144
ENV JAVA_TARBALL=server-jre-8u144-linux-x64.tar.gz
ENV JAVA_HOME=/opt/java/jdk${JAVA_VERSION}
ENV JAVA_MAGIC="090f390dda5b47b9b721c7dfaa008135"
ENV JAVA_VERSION_BUILD="8u144-b01"

# Swarm Env Variables (defaults)
ENV SWARM_MASTER=http://jenkins:8080/jenkins/
ENV SWARM_USER=jenkins
ENV SWARM_PASSWORD=jenkins

# NodeJS Variables
ENV NODEJS_VERSION=6.9.2
ENV NPM_CONFIG_LOGLEVEL info

# Slave Env Variables
ENV SLAVE_NAME="Swarm_Slave"
ENV SLAVE_LABELS="docker awscli nodejs nodejs${NODEJS_VERSION}"
ENV SLAVE_MODE="exclusive"
ENV SLAVE_EXECUTORS=4
ENV SLAVE_DESCRIPTION="Core Jenkins Slave"
ENV SWARM_CLIENT_VERSION="2.2"

# Pre-requisites
RUN yum -y install epel-release
RUN yum install -y \
    bzip2 \
    make \
    gcc \
    gcc-c++ \
    which \
    git \
    wget \
    tar \
    openldap-clients \
    openssl \
    python-pip && \
    yum clean all

RUN pip install -U pip
RUN pip install awscli==1.11.136

# Docker versions Env Variables
ENV DOCKER_ENGINE_VERSION=17.05.0.ce-1.el7.centos
ENV DOCKER_COMPOSE_VERSION=1.15.0
ENV DOCKER_MACHINE_VERSION=v0.12.2

RUN curl -fsSL https://get.docker.com/ | sed "s/docker-engine/docker-engine-${DOCKER_ENGINE_VERSION}/" | sh

RUN curl -L https://github.com/docker/compose/releases/download/${DOCKER_COMPOSE_VERSION}/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose && \
    chmod +x /usr/local/bin/docker-compose
RUN curl -L https://github.com/docker/machine/releases/download/${DOCKER_MACHINE_VERSION}/docker-machine-`uname -s`-`uname -m` >/usr/local/bin/docker-machine && \
    chmod +x /usr/local/bin/docker-machine

# Install Java
RUN wget -q --no-check-certificate --directory-prefix=/tmp --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" \
            http://download.oracle.com/otn-pub/java/jdk/${JAVA_VERSION_BUILD}/${JAVA_MAGIC}/${JAVA_TARBALL}
RUN mkdir -p /opt/java && tar -xzf /tmp/${JAVA_TARBALL} -C /opt/java/
RUN alternatives --install /usr/bin/java java /opt/java/jdk${JAVA_VERSION}/bin/java 100
RUN rm -rf /tmp/* && rm -rf /var/log/*

# Use https in git
RUN git config --global url."https://".insteadOf git://

# Install nodejs
RUN export GNUPGHOME="$(mktemp -d)" \
    # gpg keys listed at https://github.com/nodejs/node
    && for key in \
        94AE36675C464D64BAFA68DD7434390BDBE9B9C5 \
        FD3A5288F042B6850C66B31F09FE44734EB7990E \
        71DCFD284A79C3B38668286BC97EC7A07EDE3FC1 \
        DD8F2338BAE7501E3DD5AC78C273792F7D83545D \
        C4F0DFFF4E8C1A8236409D08E73BC641CC11F4C8 \
        B9AE9905FFD7803F25714661B63B535A4C206CA9 \
        56730D5401028683275BD23C23EFEFE93C4CFFFE \
    ; do \
        gpg --keyserver hkp://pgp.mit.edu:80 --recv-keys "$key" || \
        gpg --keyserver hkp://keyserver.pgp.com:80 --recv-keys "$key" || \
        gpg --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-keys "$key" ; \
    done \
    && curl -SLO "https://nodejs.org/dist/v$NODEJS_VERSION/node-v$NODEJS_VERSION-linux-x64.tar.xz" \
    && curl -SLO --compressed "https://nodejs.org/dist/v$NODEJS_VERSION/SHASUMS256.txt.asc" \
    && gpg --batch --decrypt --output SHASUMS256.txt SHASUMS256.txt.asc \
    && grep " node-v$NODEJS_VERSION-linux-x64.tar.xz\$" SHASUMS256.txt | sha256sum -c - \
    && tar -xJf "node-v$NODEJS_VERSION-linux-x64.tar.xz" -C /usr/local --strip-components=1 \
    && rm "node-v$NODEJS_VERSION-linux-x64.tar.xz" SHASUMS256.txt.asc SHASUMS256.txt \
    && ln -s /usr/local/bin/node /usr/local/bin/nodejs

RUN npm install gulp bower -g && npm install gulp && npm cache clear

# Make Jenkins a slave by installing swarm-client
RUN curl -s -o /bin/swarm-client.jar -k http://repo.jenkins-ci.org/releases/org/jenkins-ci/plugins/swarm-client/${SWARM_CLIENT_VERSION}/swarm-client-${SWARM_CLIENT_VERSION}-jar-with-dependencies.jar

# Start Swarm-Client
CMD java -jar /bin/swarm-client.jar -executors ${SLAVE_EXECUTORS} -description "${SLAVE_DESCRIPTION}" -master ${SWARM_MASTER} -username ${SWARM_USER} -password ${SWARM_PASSWORD} -name "${SLAVE_NAME}" -labels "${SLAVE_LABELS}" -mode ${SLAVE_MODE}
