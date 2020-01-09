FROM ubuntu:16.04

ENV HOME /litecoincash

ADD ./bin /usr/local/bin

ADD ./share /usr/local/share/*

RUN chmod a+x /usr/local/bin/*

VOLUME ["/litcoincash"]

EXPOSE 8332 8333

WORKDIR /litecoincash

ENTRYPOINT ["/usr/local/bin/litecoincashd"]
