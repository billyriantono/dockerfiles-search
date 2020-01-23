FROM jenkins/jnlp-slave:3.35-5

ENV DOCKER_VERSION="18.06.1"
ARG DOCKER_COMPOSE_VERSION="1.21.1"
ENV NODEJS_VERSION="12.13.1"
ENV YARN_VERSION="1.19.1"

USER root

RUN apt-get update

# Install Docker
RUN apt-get install -qq -y --no-install-recommends \
      apt-transport-https \
      ca-certificates \
      curl \
      gnupg2 \
      software-properties-common \
      xz-utils

RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add - && \
    apt-key fingerprint 0EBFCD88 && \
    add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian stretch stable" && \
    add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian stretch stable" && \
    apt-get update && \
    apt-get install -qq -y --no-install-recommends docker-ce=${DOCKER_VERSION}~ce~3-0~debian

RUN curl -L https://github.com/docker/compose/releases/download/${DOCKER_COMPOSE_VERSION}/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose && \
    chmod +x /usr/local/bin/docker-compose

# Install Node.js
RUN curl -fsSLO --compressed "https://nodejs.org/dist/v${NODEJS_VERSION}/node-v${NODEJS_VERSION}-linux-x64.tar.xz"
RUN tar -xJvf node-v${NODEJS_VERSION}-linux-x64.tar.xz -C /tmp
RUN cp -R /tmp/node-v${NODEJS_VERSION}-linux-x64/* /usr/local
RUN rm node-v${NODEJS_VERSION}-linux-x64.tar.xz

# Install Yarn package manager
RUN npm install --global yarn@${YARN_VERSION}

# Cleanup
RUN apt-get clean \
    && rm -rf /tmp/* ~/*.tgz \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /var/cache/apk/*

# Verify that everything has been installed
RUN docker -v
RUN docker-compose -v
RUN node -v
RUN npm -v
RUN yarn -v

ADD ./run.sh /usr/local/bin/run-jnlp-agent
RUN chmod +x /usr/local/bin/run-jnlp-agent

ENTRYPOINT ["run-jnlp-agent"]
