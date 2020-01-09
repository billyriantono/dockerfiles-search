FROM ubuntu

RUN sed -i 's/http\:\/\/security.ubuntu.com\/ubuntu/mirror\:\/\/mirrors.ubuntu.com\/mirrors.txt/' /etc/apt/sources.list \
    && sed -i 's/http\:\/\/extras.ubuntu.com\/ubuntu/mirror\:\/\/mirrors.ubuntu.com\/mirrors.txt/' /etc/apt/sources.list \
    && sed -i 's/http\:\/\/archive.ubuntu.com\/ubuntu/mirror\:\/\/mirrors.ubuntu.com\/mirrors.txt/' /etc/apt/sources.list
