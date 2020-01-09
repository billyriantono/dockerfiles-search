FROM debian:stretch-slim

RUN apt-get update && apt-get install -y curl

# https://devcenter.heroku.com/articles/heroku-cli#other-installation-methods
RUN curl https://cli-assets.heroku.com/install.sh | sh

# https://circleci.com/docs/2.0/building-docker-images/
RUN curl -L -o /tmp/docker-18.06.1-ce.tgz \
    https://download.docker.com/linux/static/stable/x86_64/docker-18.06.1-ce.tgz \
    && tar -xz -C /tmp -f /tmp/docker-18.06.1-ce.tgz \
    && mv /tmp/docker/* /usr/bin
