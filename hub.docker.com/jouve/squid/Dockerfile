FROM alpine:3.10

RUN apk add --no-cache squid

RUN mkdir /etc/squid.d && mv /etc/squid/squid.conf /etc/squid.d

COPY squid.conf /etc/squid/squid.conf

EXPOSE 3128

CMD [ "squid",  "-N", "-d", "999" ]

