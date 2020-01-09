FROM debian:8
MAINTAINER Pin <pinfake@hotmail.com>
RUN apt-get update && \
    apt-get install -y curl git build-essential ca-certificates php5-cli php5-redis php5-curl php5-mcrypt php-pear && \
    curl -sL https://deb.nodesource.com/setup_6.x | bash - && \ 
    apt-get install -y nodejs
RUN mkdir -p /root/.ssh && \
    printf "Host gitlab.antevenio.com\n\tHostName gitlab.antevenio.com\n\tPort 2222" > /root/.ssh/config
