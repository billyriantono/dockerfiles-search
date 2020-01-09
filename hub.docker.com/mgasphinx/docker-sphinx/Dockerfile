FROM thomasweise/docker-texlive-full
MAINTAINER Christophe CHAUVET <christophe.chauvet+docker@gmail.com>

# Usage:
# docker run -it -v <your directory>:/documents/

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get clean &&\
    apt-get update &&\
    apt-get autoclean -y &&\
    apt-get autoremove -y &&\
    apt-get update &&\
    apt-get install -f -y tzdata &&\
    apt-get install -y -q python-sphinx \
                          build-essential \
                          python-pip && \
    # clean up all temporary files
    apt-get clean &&\
    apt-get autoclean -y &&\
    apt-get autoremove -y &&\
    apt-get clean &&\
    rm -rf /tmp/* /var/tmp/* &&\
    rm -rf /var/lib/apt/lists/* &&\
    rm -f /etc/ssh/ssh_host_*

RUN mkdir documents

WORKDIR /documents
VOLUME /documents

CMD ["/bin/bash"]
