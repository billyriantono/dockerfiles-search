FROM microsoft/dotnet:1.1.1-sdk

MAINTAINER Steve Vallis <vallis@polynomial.co.uk>

LABEL vendor="Polynomial"
LABEL uk.co.polynomial.version="1.1.1"
LABEL uk.co.polynomial.release-date="2017-03-07"

RUN apt-get update && apt-get install -y nodejs && \
    update-alternatives --install /usr/bin/node nodejs /usr/bin/nodejs 100 && \
    curl https://www.npmjs.com/install.sh | sh && \
    npm install gulp -g
ENV LANG en_GB.UTF-8
ENV LANGUAGE en_GB:en
ENV LC_ALL en_GB.UTF-8
