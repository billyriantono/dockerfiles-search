FROM alpine:latest as builder
RUN apk --update add alpine-sdk yajl yajl-dev autoconf automake flex bison libtool pkgconfig linux-headers
RUN git clone https://github.com/collectd/collectd.git
WORKDIR collectd/
RUN ./build.sh
RUN ./configure --enable-ceph
RUN make
RUN make install

FROM alpine:latest
WORKDIR /opt
RUN apk --no-cache add ca-certificates
RUN apk --update add yajl
COPY --from=builder /opt/collectd/ .
VOLUME /opt/collectd/etc/
CMD /opt/sbin/collectd -f
