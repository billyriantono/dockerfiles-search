FROM jenkinsci/ssh-slave
LABEL MAINTAINER="Robert Rick <rob@myhireapp.com>"

RUN apt-get update \
  && apt-get install --no-install-recommends -y curl \
  && curl -sL https://deb.nodesource.com/setup_12.x | bash \
  && apt-get install -y nodejs zip \
  && rm -rf /var/lib/apt/lists/*
