FROM busybox:glibc
ENV FCLI_VER=v0.19
RUN wget https://gosspublic.alicdn.com/fcli/fcli-${FCLI_VER}-linux-amd64.zip \
    && unzip fcli-${FCLI_VER}-linux-amd64.zip \
    && mv fcli /usr/sbin/ \
    && rm -f fcli-${FCLI_VER}-linux-amd64.zip

ENTRYPOINT [ "/usr/sbin/fcli" ]