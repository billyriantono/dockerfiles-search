FROM gitlab/dind
MAINTAINER Diego Gullo <diego_gullo@bizmate.biz>

RUN apt-get update  && apt-get install -y make \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*
