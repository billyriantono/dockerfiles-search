FROM debian:buster

RUN apt-get -yqq update && apt-get install -yqq openssh-client git git-lfs curl docker.io
RUN apt-get -yqq clean

# The debian packages pull into dependencies that break docker login, see
# https://github.com/docker/compose/issues/6023 and others.
RUN curl -L "https://github.com/docker/compose/releases/download/1.24.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
RUN chmod +x /usr/local/bin/docker-compose
