FROM alpine as builder

WORKDIR /root/
RUN apk add --no-cache git automake autoconf asciidoc build-base
RUN git clone https://github.com/tinyproxy/tinyproxy
RUN cd tinyproxy && ls && ./autogen.sh
RUN cd tinyproxy && ./configure --prefix= --enable-filter --enable-transparent
RUN cd tinyproxy && make
RUN cd tinyproxy && make install

FROM alpine:latest
WORKDIR /
COPY --from=builder /root/tinyproxy/src/tinyproxy /
ADD files/ / 
ENTRYPOINT [ "/tinyproxy", "-d"]
