FROM alpine:latest

MAINTAINER Marcel Hanusa <mhanu@web.de>

RUN apk update
RUN apk add alpine-sdk bison

ADD msqld-tcp.patch /tmp/
WORKDIR /tmp
RUN wget http://www.hughes.com.au/downloads/msql/msql-4.1.tar.gz

RUN tar -xzf msql-4.1.tar.gz

WORKDIR /tmp/msql-4.1/src/msqld/main
RUN patch < /tmp/msqld-tcp.patch

WORKDIR /tmp/msql-4.1
RUN ./setup
RUN make all
RUN make install

RUN apk del alpine-sdk bison
RUN rm -rf /tmp/*

EXPOSE 1114

WORKDIR /opt/msql

RUN sed 's/Remote_Access = False/Remote_Access = True/g' -i etc/msql.conf
RUN sed 's/Host_Lookup = True/Host_Lookup = False/g' -i etc/msql.conf
RUN sed 's/mSQL_User = daemon/mSQL_User = root/g' -i etc/msql.conf

CMD ["bin/msqld"]
