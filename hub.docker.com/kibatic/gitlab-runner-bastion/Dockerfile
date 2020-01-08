FROM gitlab/gitlab-runner:v12.0.1

RUN curl -L https://github.com/docker/machine/releases/download/v0.16.1/docker-machine-`uname -s`-`uname -m` >/tmp/docker-machine &&\
    install /tmp/docker-machine /usr/local/bin/docker-machine
