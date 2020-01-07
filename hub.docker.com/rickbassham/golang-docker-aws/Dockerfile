FROM golang:stretch

RUN apt-get update && apt-get install -y \
    jq \
    python-pip apt-transport-https ca-certificates wget software-properties-common

RUN curl -s https://download.docker.com/linux/debian/gpg | apt-key add -

RUN apt-add-repository 'deb https://download.docker.com/linux/debian stretch stable'

RUN apt-get update && apt-get install -y docker-ce docker-compose

RUN pip install awscli --upgrade

RUN curl -sL https://deb.nodesource.com/setup_11.x | bash -

RUN apt-get install -y nodejs

RUN rm -rf /var/lib/apt/lists/*
