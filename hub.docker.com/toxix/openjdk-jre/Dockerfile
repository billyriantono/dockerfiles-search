# Dockerfile that create a base image for installing and running things that need an openjdk-jre

FROM debian:stable

# Running apt-get in noninteractive mode
#ENV DEBIAN_FRONTEND noninteractive


# Install openjdk jre
RUN    apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -qq --no-install-recommends openjdk-7-jre-headless default-jre-headless \
    && apt-get clean -qq \
    && rm -rf /var/lib/{apt,dpkg,cache,log}/

ENV JAVA_HOME /usr/lib/jvm/java-7-openjdk-amd64

# unset the apt-get environment
#ENV DEBIAN_FRONTEND [""]
