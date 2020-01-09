FROM alpine
MAINTAINER Jacques Moati <jacques@moati.net>


ARG VERSION=11.77

RUN cd /tmp && \
    apk --update add perl && \
    wget https://exiftool.org/Image-ExifTool-$VERSION.tar.gz && \
    tar -xzvf Image-ExifTool-*.tar.gz && \
    rm -rf Image-ExifTool-*.tar.gz && \
    cd Image-ExifTool-* && \
    rm -rf html t Change Makefile.PL MANIFEST META.json META.yml perl-Image-ExifTool.spec README && \
    mv * /usr/local/bin/ && \
    rm -rf /tmp/Image-ExifTool-*
