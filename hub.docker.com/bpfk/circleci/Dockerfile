FROM alpine:3.10.1
RUN apk --no-cache add bash binutils-gold build-base curl-dev docker docker-compose git \
    libcurl libsodium-dev openssh-client openssl openssl-dev sqlite-dev zlib-dev
COPY --from=bpfk/pkgbuilder:latest --chown=root:root /home/effortman/.abuild/*.rsa.pub /etc/apk/keys/
COPY --from=bpfk/ldc:latest /root/packages/ /root/packages/
COPY --from=bpfk/dub:latest /root/packages/ /root/packages/
RUN apk --no-cache add /root/packages/effortman/x86_64/ldc-1.16.0-r0.apk \
    /root/packages/effortman/x86_64/ldc-runtime-1.16.0-r0.apk \
    /root/packages/effortman/x86_64/ldc-static-1.16.0-r0.apk \
    /root/packages/effortman/x86_64/dub-1.17.0-r0.apk \
    /root/packages/effortman/x86_64/dtools-rdmd-2.087.1-r0.apk \
    && rm -rf /root/packages/
