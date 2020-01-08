FROM debian:wheezy

RUN apt-get update && apt-get install -y \
    sudo \
    adduser \
    procps \ 
    net-tools \
    apt-utils \
    ca-certificates \
    vim \
    wget \
    curl \
    git \
    make

COPY .bashrc /root/

CMD ["/bin/bash"]
