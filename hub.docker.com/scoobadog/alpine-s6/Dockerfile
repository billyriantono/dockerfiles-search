FROM alpine:3.6
MAINTAINER Janne K <0x022b@gmail.com>
ADD lib/s6-overlay-amd64.tar.gz /
RUN find / -perm /06000 -type f -xdev -exec chmod a-s {} \;
ENTRYPOINT ["/init"]
