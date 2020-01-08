FROM jenkins
MAINTAINER Thomas Gerlach <info@talixa.com>

USER root
RUN apt-get update && \
    apt-get install -y build-essential && \
    apt-get install -y lib32z1 && \
    apt-get install -y lib32stdc++6
USER jenkins
