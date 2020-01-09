FROM ubuntu:14.04
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update \ 
    && apt-get install -y curl \
    && apt-get install -y nmap \
    && apt-get install -y socat \
    && apt-get install -y openssh-client \
    && apt-get install -y openssl \
    && apt-get install -y iotop \
    && apt-get install -y strace \
    && apt-get install -y tcpdump \
    && apt-get install -y lsof \
    && apt-get install -y inotify-tools \
    && apt-get install -y sysstat \
    && apt-get install -y build-essential \
    && echo "source /root/bash_extra" >> /root/.bashrc
ADD bash_extra /root/bash_extra
CMD ["/bin/bash"]
