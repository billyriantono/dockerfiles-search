FROM circleci/node:8.15.0

USER 0
RUN apt-get update && apt-get install -y \
    openjdk-8-jre \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*
RUN npm i -g npm@6.6.0
RUN npm i -g firebase-tools@6.3.0
RUN firebase setup:emulators:firestore
RUN curl -L https://github.com/tcnksm/ghr/releases/download/v0.12.0/ghr_v0.12.0_linux_amd64.tar.gz \
  > /tmp/ghr.tar.gz
RUN tar -C /tmp -xf /tmp/ghr.tar.gz
RUN mv /tmp/ghr_v0.12.0_linux_amd64/ghr /usr/local/bin
RUN rm -fr /tmp/ghr_v0.12.0_linux_amd64
USER 3434
