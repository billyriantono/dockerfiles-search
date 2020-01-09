FROM ubuntu:18.10
MAINTAINER Ivan Zakharin <ivan.turest@gmail.com>
RUN apt update &&\
    apt install -y sysstat
USER root
WORKDIR /
COPY ./metrics.sh /usr/bin/metrics
ENTRYPOINT ["metrics"]