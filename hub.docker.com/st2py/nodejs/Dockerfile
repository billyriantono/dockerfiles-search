FROM debian:wheezy

ENV NODE_VERSION 0.10.33
ENV NPM_VERSION 2.1.8

RUN apt-get update \
    && apt-get -y dist-upgrade \
    && apt-get install -y curl ca-certificates --no-install-recommends \
    && curl -sL https://deb.nodesource.com/setup | bash - \
    && apt-get install -y nodejs npm build-essential \
    && npm install -g npm@"$NPM_VERSION" \
    && npm cache clear \
    && apt-get clean \
    && apt-get autoclean \
    && apt-get autoremove -y \
    && rm -rf /var/lib/apt/lists/*

RUN apt-get update \
    && mkdir /var/nodejs \
    && curl -OSL https://github.com/st2py/NodeJs/raw/master/app.js \
    && mv app.js /var/nodejs/ \
    && apt-get purge -y --auto-remove curl ca-certificates \
    && apt-get clean \
    && apt-get autoclean \
    && apt-get autoremove -y \
    && rm -rf /var/lib/apt/lists/*
    
RUN touch /etc/run.sh \
    && chmod a+x /etc/run.sh \
    && echo "#!/bin/sh" > /etc/run.sh \
    && echo "" >> /etc/run.sh \
    && echo "nodejs /var/nodejs/app.js" >> /etc/run.sh

EXPOSE 80
CMD ["/etc/run.sh"]
