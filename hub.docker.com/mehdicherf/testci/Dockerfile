# small alpine image
FROM alpine
RUN apk add --update --no-cache  \
      openssl \
      curl \
      wget \
      unzip \
      bash \
      nodejs \
      nodejs-npm \
      openjdk8-jre

#PMD version
ENV PMD_VERSION=6.13.0

# install latest sfdx from npm
RUN npm install sfdx-cli --global
RUN sfdx --version
RUN sfdx plugins --core

# install PMD
RUN wget https://github.com/pmd/pmd/releases/download/pmd_releases%2F6.13.0/pmd-bin-6.13.0.zip && \
    unzip pmd-bin-6.13.0.zip && \
    rm pmd-bin-*.zip && \
    alias pmd="pmd-bin-6.13.0/bin/run.sh pmd"

ENV PMD_BINARY pmd-bin-5.3.3/bin/run.sh