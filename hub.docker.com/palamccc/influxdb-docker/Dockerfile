FROM alpine
RUN apk add --no-cache wget ca-certificates \
  && wget -q -O /etc/apk/keys/sgerrand.rsa.pub \
       https://raw.githubusercontent.com/sgerrand/alpine-pkg-glibc/master/sgerrand.rsa.pub \
  && wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.23-r3/glibc-2.23-r3.apk \
  && apk add glibc-2.23-r3.apk \
  && rm glibc-2.23-r3.apk /etc/apk/keys/sgerrand.rsa.pub \
  && wget https://dl.influxdata.com/influxdb/releases/influxdb-1.0.2_linux_amd64.tar.gz \
  && tar xf influxdb-1.0.2_linux_amd64.tar.gz \
  && mv ./influxdb-1.0.2-1/usr/bin/influxd / \
  && rm -Rf influxdb-1.0.2-1 influxdb-1.0.2_linux_amd64.tar.gz \
  && apk del wget
