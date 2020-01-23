FROM debian:stretch

ENV NGINX_VERSION 1.13.8
ENV NGINX_RTMP_VERSION 1.2.1
ENV FFMPEG_VERSION 3.3.4

RUN mkdir -p /opt/data && mkdir /www

RUN  echo "deb http://deb.debian.org/debian stretch main contrib non-free" > /etc/apt/sources.list \
  && echo "deb-src http://deb.debian.org/debian stretch main contrib non-free" >> /etc/apt/sources.list \
  && echo "deb http://deb.debian.org/debian stretch-updates main contrib non-free" >> /etc/apt/sources.list \
  && echo "deb-src http://deb.debian.org/debian stretch-updates main contrib non-free" >> /etc/apt/sources.list \
  && echo "deb http://security.debian.org stretch/updates main contrib non-free" >> /etc/apt/sources.list \
  && echo "deb-src http://security.debian.org stretch/updates main contrib non-free" >> /etc/apt/sources.list \
  && echo "deb http://www.deb-multimedia.org stretch main" >> /etc/apt/sources.list \
  && echo "deb-src http://www.deb-multimedia.org stretch main" >> /etc/apt/sources.list

RUN apt-get update \
  && apt-get install -y --allow-unauthenticated --no-install-recommends build-essential openssl ca-certificates libpcre++-dev libpcre3-dev zlib1g-dev wget git tar gzip libfdk-aac-dev librtmp-dev libwebp-dev libfreetype6-dev libass-dev libopus-dev \
  && apt-get build-dep -y --allow-unauthenticated --no-install-recommends nginx ffmpeg

# Get nginx source.
RUN cd /tmp && wget http://nginx.org/download/nginx-${NGINX_VERSION}.tar.gz \
  && tar zxf nginx-${NGINX_VERSION}.tar.gz \
  && rm nginx-${NGINX_VERSION}.tar.gz

# Get nginx-rtmp module.
RUN cd /tmp && wget https://github.com/arut/nginx-rtmp-module/archive/v${NGINX_RTMP_VERSION}.tar.gz \
  && tar zxf v${NGINX_RTMP_VERSION}.tar.gz && rm v${NGINX_RTMP_VERSION}.tar.gz

# Compile nginx with nginx-rtmp module.
RUN cd /tmp/nginx-${NGINX_VERSION} \
  && ./configure \
  --prefix=/opt/nginx \
  --add-module=/tmp/nginx-rtmp-module-${NGINX_RTMP_VERSION} \
  --conf-path=/opt/nginx/etc/nginx.conf --error-log-path=/opt/nginx/logs/error.log --http-log-path=/opt/nginx/logs/access.log \
  --with-debug
RUN cd /tmp/nginx-${NGINX_VERSION} && make && make install

# Get ffmpeg source.
RUN cd /tmp/ && wget http://ffmpeg.org/releases/ffmpeg-${FFMPEG_VERSION}.tar.gz \
  && tar zxf ffmpeg-${FFMPEG_VERSION}.tar.gz && rm ffmpeg-${FFMPEG_VERSION}.tar.gz

# Compile ffmpeg.
RUN cd /tmp/ffmpeg-${FFMPEG_VERSION} && \
  ./configure \
  --enable-version3 \
  --enable-gpl \
  --enable-nonfree \
  --enable-small \
  --enable-libmp3lame \
  --enable-libx264 \
  --enable-libx265 \
  --enable-libvpx \
  --enable-libtheora \
  --enable-libvorbis \
  --enable-libopus \
  --enable-libfdk-aac \
  --enable-libass \
  --enable-libwebp \
  --enable-librtmp \
  --enable-postproc \
  --enable-avresample \
  --enable-libfreetype \
  --enable-openssl \
  --disable-debug \
  && make && make install && make distclean

# Cleanup.
RUN apt-get -y purge build-essential && apt-get autoremove --purge -y
RUN rm -rf /var/cache/apt/* /tmp/*

ADD nginx.conf /opt/nginx/etc/nginx.conf
ADD static /www/static

CMD ["/opt/nginx/sbin/nginx"]
