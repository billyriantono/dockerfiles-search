FROM phusion/baseimage
MAINTAINER Ravenium <ravenium@gmail.com>

ENV DEBIAN_FRONTEND noninteractive
ENV PATH=$PATH:/usr/local/nginx/sbin

# create directories
RUN mkdir -p /src && \ 
  mkdir -p /config && \
  mkdir -p /logs && \
  mkdir -p /recordings && \ 
  chmod -R 777 /recordings

# Run updates and install dependencies
RUN apt-get update && \
  apt-get install -y \ 
  build-essential \
  wget \
  libpcre3-dev \
  zlib1g-dev \
  libssl-dev

# get nginx source and pick up after ourselves
WORKDIR /src
RUN wget http://nginx.org/download/nginx-1.15.0.tar.gz && \
  tar zxf nginx-1.15.0.tar.gz && \
  rm nginx-1.15.0.tar.gz

# get nginx-rtmp module
RUN wget https://github.com/arut/nginx-rtmp-module/archive/v1.2.1.tar.gz && \
  tar zxf v1.2.1.tar.gz && \
  rm v1.2.1.tar.gz

# compile nginx with rtmp
WORKDIR /src/nginx-1.15.0
RUN ./configure \
  --add-module=/src/nginx-rtmp-module-1.2.1 \
  --conf-path=/config/nginx.conf \
  --error-log-path=/logs/error.log \
  --http-log-path=/logs/access.log
RUN make && \
  make install

# remove the source to reduce image size
WORKDIR /config
RUN rm -rf /src
COPY ./nginx.conf nginx.conf
COPY ./stat.xsl stat.xsl

VOLUME ["/config"]
VOLUME ["/recordings"]

EXPOSE 1935
EXPOSE 8080

WORKDIR /logs
RUN ln -s /dev/stdout access.log
RUN ln -s /dev/stderr error.log

ENTRYPOINT ["nginx"]
CMD ["-g", "daemon off;"]
