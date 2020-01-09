FROM openjdk:8-jdk

RUN unlink /bin/sh && ln -s /bin/bash /bin/sh \
    && apt-get update \
    && apt-get install -y curl \
    && apt-get -y autoclean

ENV PYTHONIOENCODING=UTF-8
ENV AWS_CLI_VERSION 1.11.167

RUN apt-get -y install python python-pip python-setuptools ca-certificates groff less && \
    pip --no-cache-dir install awscli==${AWS_CLI_VERSION}

ENV NVM_DIR /usr/local/nvm
ENV NODE_VERSION 8.6.0

RUN curl --silent -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.2/install.sh | bash \
    && source $NVM_DIR/nvm.sh \
    && nvm install $NODE_VERSION \
    && nvm alias default $NODE_VERSION \
    && nvm use default \
    && curl -L https://services.gradle.org/distributions/gradle-3.0-bin.zip -o gradle-3.0-bin.zip \
    && apt-get install -y unzip \
    && unzip gradle-3.0-bin.zip

ENV GRADLE_HOME=/gradle-3.0
ENV PATH=$PATH:$GRADLE_HOME/bin
ENV NODE_PATH $NVM_DIR/v$NODE_VERSION/lib/node_modules
ENV PATH $NVM_DIR/versions/node/v$NODE_VERSION/bin:$PATH

