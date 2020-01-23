FROM alpine

LABEL maintainer="heywoodlh"

#Telnet and netcat installation
RUN apk add busybox-extras netcat-openbsd

#Masscan installation
RUN apk add clang gcc libc-dev git make libc6-compat libpcap-dev linux-headers && \
    cd /tmp && \
    git clone https://github.com/robertdavidgraham/masscan && \
    cd masscan && \
    make -j && \
    mv bin/masscan /usr/local/bin && \
    rm -rf /tmp/masscan && \
    apk del clang git make linux-headers libc-dev gcc


RUN mkdir /data

CMD "/bin/ash"
