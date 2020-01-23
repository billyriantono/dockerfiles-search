FROM ubuntu:14.04
MAINTAINER Evgeniy A. Cymbalyuk <cimbaluk@saber3d.ru>

# link: https://docs.docker.com/engine/installation/linux/ubuntu/
RUN set -ex                           \
    && apt-get update                 \
    && apt-get install -y             \
        apt-transport-https           \
        ca-certificates               \
        curl                          \
        software-properties-common    \
    && (curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -) \
    && add-apt-repository             \
        "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
        $(lsb_release -cs) stable"    \
    && apt-get update                 \
    && apt-get install -y docker-ce   \
    && apt-get remove -y              \
        curl                          \
        ca-certificates               \
        software-properties-common    \
    && apt-get autoremove -y          \
    && rm -rf /var/lib/apt/lists/*
