FROM ubuntu:15.10
MAINTAINER "Michele Bariani" <michele.bariani@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && \
    apt-get -y install \
       curl \
       openjdk-7-jre-headless \
       && \
    apt-get clean all && \
    useradd -m openrefine && \
    cd /home/openrefine && \
    curl -L https://github.com/OpenRefine/OpenRefine/releases/download/2.6-rc.2/openrefine-linux-2.6-rc.2.tar.gz | tar -xz && \
    chown -R openrefine. openrefine-2.6-rc.2

USER openrefine
WORKDIR /home/openrefine/openrefine-2.6-rc.2
ENTRYPOINT ./refine -i 0.0.0.0
EXPOSE 3333

