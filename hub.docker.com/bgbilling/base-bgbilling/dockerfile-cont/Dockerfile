# beyondthestory/fuskei Dockerfile

FROM beyondthestory/java8
MAINTAINER Darrin Wortlehock <darrin@beyondthestory.com>

ENV HOME /root
RUN mkdir -p /build
ADD . /build
RUN /build/scripts/install.sh
CMD ["/sbin/my_init"]

VOLUME /data

EXPOSE 3030