FROM alpine as builder
RUN apk update
RUN apk add git libressl-dev autoconf automake libtool build-base linux-headers python-dev bash

RUN git clone https://github.com/facebook/watchman.git
WORKDIR /watchman

RUN git checkout v4.9.0
RUN ./autogen.sh
RUN ./configure --enable-lenient
RUN make
RUN make install

FROM alpine
COPY --from=builder /usr/local/bin/watchman* /usr/local/bin/
COPY --from=builder /usr/local/share/doc/watchman-4.9.0 /usr/local/share/doc/watchman-4.9.0
COPY --from=builder /usr/local/var/run/watchman /usr/local/var/run/watchman
