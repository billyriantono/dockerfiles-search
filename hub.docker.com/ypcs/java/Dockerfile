FROM ypcs/debian:buster

RUN /usr/lib/docker-helpers/apt-setup && \
    /usr/lib/docker-helpers/apt-upgrade && \
    apt-get --assume-yes install \
        default-jre-headless && \
    /usr/lib/docker-helpers/apt-cleanup

