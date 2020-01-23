# beyondthestory/java Dockerfile

FROM beyondthestory/baseimage-docker
MAINTAINER Darrin Wortlehock <darrin@beyondthestory.com>

ENV HOME /root
RUN mkdir -p /build
ADD . /build

RUN chmod +x /build/scripts/*.sh && sleep 1 && /build/scripts/install.sh

CMD ["/sbin/my_init"]
