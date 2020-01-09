FROM alpine:3.2
MAINTAINER Zenreach Engineering <engineering@zenreach.com>
VOLUME /tmp
RUN apk add --update ca-certificates openssl && \
    wget https://github.com/rlmcpherson/s3gof3r/releases/download/v0.4.10/gof3r_0.4.10_linux_amd64.tar.gz -O - | tar -xz && \
    mv gof3r_0.4.10_linux_amd64/gof3r /usr/bin/ && \
    rmdir gof3r_0.4.10_linux_amd64/ && \
    apk del --purge openssl
ADD gof3r.ini /root/.gof3r.ini
ADD s3cat /usr/bin/
RUN chmod 755 /usr/bin/s3cat
ENTRYPOINT ["/usr/bin/s3cat"]
