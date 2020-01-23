FROM maven:3-jdk-8

RUN set -ex; \
    # apt update -qq;\
    # apt install openssh -y;\
    wget https://download.docker.com/linux/static/stable/x86_64/docker-19.03.5.tgz -O /tmp/docker-19.03.5.tgz;\
    cd /tmp;\
    tar -xf docker-19.03.5.tgz;\
    cp /tmp/docker/docker /usr/bin;\
    rm -fr /var/lib/apt/lists/* /tmp/* /var/tmp/* /var/cache/apt/archives/*;
