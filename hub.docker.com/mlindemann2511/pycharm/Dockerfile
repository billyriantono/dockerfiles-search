FROM ubuntu:xenial 

ENV PYCHARM_VERSION 2017.3.2 
ENV DISPLAY=10.0.75.1:0.0
ENV NETWORK=host

RUN apt-get update && \
    apt-get install -y --no-install-recommends curl openjdk-8-jdk python python3.5 git && \
    apt-get clean all
	
RUN mkdir /home/dev && \
    useradd dev -d /home/dev && \
    curl http://download-cf.jetbrains.com/python/pycharm-community-${PYCHARM_VERSION}.tar.gz > /home/dev/pycharm-community-${PYCHARM_VERSION}.tar.gz && \
    chown -R dev:dev /home/dev && \
    cd /home/dev && \
    tar xvzf pycharm-community-${PYCHARM_VERSION}.tar.gz && \
    rm -f pycharm-community-${PYCHARM_VERSION}.tar.gz && \
    mv /home/dev/pycharm* /home/dev/pycharm

USER dev 

VOLUME /home/dev

ENTRYPOINT [ "/home/dev/pycharm/bin/pycharm.sh" ]