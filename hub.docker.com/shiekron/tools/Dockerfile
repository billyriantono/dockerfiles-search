FROM ubuntu:14.04

# info
MAINTAINER Joe Ortiz version: 0.3

# update container
RUN apt-get update && \
    apt-get install -y python-software-properties \
                       software-properties-common && \
    add-apt-repository ppa:cernekee/ppa && \
    apt-get update && \
    apt-get install -y stoken \
                       libstoken-dev \
                       openconnect \
                       ocproxy \
                       openvpn && \
    apt-get autoclean

COPY assets/init /app/init
EXPOSE 2280
RUN chmod 755 /app/init
ENTRYPOINT ["/app/init"]
