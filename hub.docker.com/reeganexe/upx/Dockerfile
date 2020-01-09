FROM alpine:3.8

RUN wget -qO- https://github.com/upx/upx/releases/download/v3.95/upx-3.95-amd64_linux.tar.xz | tar Jx && \
    mv upx-3.95-amd64_linux/upx /usr/local/bin/ && \
    rm -rf upx-3.95-amd64_linux

ENTRYPOINT ["upx", "--best"]
