FROM ubuntu:xenial
MAINTAINER yasuyuky <yasuyuki.ymd@gmail.com>

RUN apt-get -y update \
&&  apt-get -y install \
                       pandoc \
                       fontconfig \
                       zlib1g \
                       libfreetype6 \
                       libx11-6 \
                       libxext6 \
                       libxrender1 \
                       tar \
                       xz-utils \
                       language-pack-ja \
                       fonts-ipaexfont \
                       fonts-takao \
                       fonts-noto \
                       fonts-mplus \
                       fonts-mathjax \
                       wget
WORKDIR /opt
RUN wget https://downloads.wkhtmltopdf.org/0.12/0.12.4/wkhtmltox-0.12.4_linux-generic-amd64.tar.xz \
&& tar xf wkhtmltox-0.12.4_linux-generic-amd64.tar.xz \
&& cp wkhtmltox/bin/wkhtmlto* /usr/bin/ \
&& rm -rf wkhtmltox*
RUN mkdir /work /assets
WORKDIR /work
COPY assets/conv.sh /bin/conv
COPY assets/doc.css /assets
ENV LANG ja_JP.UTF-8
CMD ["bash"]
