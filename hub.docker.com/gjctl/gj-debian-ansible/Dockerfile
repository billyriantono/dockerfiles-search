FROM debian:10-slim
LABEL maintainer="Guillermo Jury"
RUN apt-get update && apt-get install -y \
    vim \
    ssh \
    net-tools \
    python2 \
    python3 \
    python-pip \
    python3-pip \
    git\
    wget \
    curl \
    inetutils-ping\
    ansible     
ADD .bashrc /root/.bashrc
ENTRYPOINT [ "bash" ]