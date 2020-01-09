FROM sylvaindeloux/php:7.2-cli
MAINTAINER Sylvain Deloux <docker@eax.fr>


ENV DEBIAN_FRONTEND noninteractive


RUN apt-get update && \
    apt-get install -y gnupg && \
    curl -sL https://deb.nodesource.com/setup_10.x | bash - && \
    apt-get install -y nodejs && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
