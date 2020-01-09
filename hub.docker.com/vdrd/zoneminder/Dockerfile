FROM alpine AS buildzone

RUN apk --no-cache add build-base cmake git openssh-client \
    v4l-utils-dev libexecinfo-dev zlib-dev libcurl libjpeg-turbo linux-headers

RUN git clone --recursive https://github.com/ZoneMinder/zoneminder.git

WORKDIR /zoneminder

RUN apk --no-cache add libjpeg-turbo-dev curl-dev
RUN apk --no-cache add mariadb-client mariadb-dev
RUN apk --no-cache add perl perl-dbi perl-dbd-mysql perl-date-manip\
    perl-lwp-useragent-determined perl-sys-mmap
RUN apk --no-cache add pcre-dev libgcrypt-dev gnutls-dev x264-dev \
    ffmpeg-dev vlc-dev
# libmp4v2 is missing in alpine linux

#RUN cmake -DCURL_LIBRARY=/usr/lib \
#    -DJPEG_LIBRARY=/usr/lib \
#    .
RUN cmake .
RUN make