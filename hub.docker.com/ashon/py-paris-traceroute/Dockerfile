FROM python:3.7.3 as builder

WORKDIR /opt/py-paris-traceroute

RUN apt-get update && \
    apt-get install -qy \
        libtool \
        automake

ADD https://paris-traceroute.net/downloads/paris-traceroute-0.92-dev.tar.gz ./
RUN tar -zxf paris-traceroute-0.92-dev.tar.gz

WORKDIR /opt/py-paris-traceroute/paris-traceroute-current
RUN ./autogen.sh
RUN ./configure
RUN make install

# Copy paris-traceroute from builder
FROM python:3.7.3

WORKDIR /opt/py-paris-traceroute
COPY --from=builder \
    /usr/local/bin/paris-traceroute \
    /usr/local/bin/paris-traceroute

CMD ["./paris-traceroute"]
