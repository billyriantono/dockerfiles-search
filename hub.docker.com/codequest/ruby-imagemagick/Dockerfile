FROM ruby:2.3.3

ENV IMAGEMAGICK_VERSION 7.0.3-10

RUN wget http://ftp.nluug.nl/ImageMagick/ImageMagick-${IMAGEMAGICK_VERSION}.tar.gz && \
    tar xvzf ImageMagick-${IMAGEMAGICK_VERSION}.tar.gz --directory /tmp

WORKDIR /tmp/ImageMagick-${IMAGEMAGICK_VERSION}

RUN autoconf && \
    ./configure && \
    make && \
    make install && \
    ldconfig /usr/local/lib && \
    rm -rf /tmp/ImageMagick-${IMAGEMAGICK_VERSION}
