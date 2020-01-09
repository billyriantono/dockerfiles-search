# get base images
FROM ubuntu

# update and install good stuff
RUN apt-get update && apt-get install -y \
    curl \
    ffmpeg \
    git \
    lvm2\
    man \
    nano \
    openssl \
    tree \
    wget
    
# set up home dir
RUN mkdir -p /home/lnxnv
WORKDIR /home/lnxnv

