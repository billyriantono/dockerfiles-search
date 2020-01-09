##reference from internap/cloudfuse
##https://hub.docker.com/r/internap/cloudfuse/

#base OS
FROM sato0203/docker-master:latest_base

# setup conohaSwift
RUN apt-get update -y && \
    apt-get upgrade -y && \
    apt-get install -y wget build-essential libcurl4-openssl-dev libxml2-dev libssl-dev libfuse-dev libjson-c-dev wget pkg-config fuse && \
    wget https://github.com/redbo/cloudfuse/archive/master.tar.gz && \
    tar -xf master.tar.gz && \
    cd cloudfuse-master && \
    ./configure && make && make install
