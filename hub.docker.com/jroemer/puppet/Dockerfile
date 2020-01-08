# Puppet

FROM ubuntu:18.04
LABEL maintainer "Jonathan Roemer <dev@roemersoftworks.com>"

RUN apt-get update && apt-get install -y software-properties-common
RUN add-apt-repository ppa:neovim-ppa/stable && apt-get update && \
    apt-get -y upgrade && apt-get install -y --no-install-recommends \
    python3 python3-pip python3-dev python3-setuptools neovim puppet ansible \
    curl shellcheck git puppet-lint ansible-lint

ENTRYPOINT [ "/bin/bash" ]
