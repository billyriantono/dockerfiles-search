FROM ubuntu:18.04
MAINTAINER Andre Pereira andrespp@gmail.com

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && \
    apt-get install -y texlive-full build-essential && \
    apt-get clean && rm -rf /var/lib/apt/list && \
    mkdir /latex

WORKDIR /latex

VOLUME ["/latex"]

CMD ["/bin/bash"]
