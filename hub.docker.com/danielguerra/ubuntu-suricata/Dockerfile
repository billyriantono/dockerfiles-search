FROM ubuntu:18.04
MAINTAINER Daniel Guerra
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update
RUN apt-get install -y apt-utils software-properties-common
RUN add-apt-repository ppa:oisf/suricata-stable
RUN apt-get update
RUN apt-get install -y suricata && apt clean
CMD /bin/bash
