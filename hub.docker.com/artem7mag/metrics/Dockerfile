FROM ubuntu:16.04
MAINTAINER "Artem Martynenko" <artem7mag@gmail.com>

COPY metrics /usr/bin

RUN apt-get update && \
    apt-get install --no-install-recommends -y  sysstat gawk && \
    apt-get upgrade -y && \
    apt-get clean && \
    apt-get autoremove
 
ENTRYPOINT ["metrics"]
