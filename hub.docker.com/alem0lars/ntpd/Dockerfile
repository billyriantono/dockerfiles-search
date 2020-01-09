FROM alpine:latest

RUN apk update
RUN apk add openntpd

ADD dist/ntpd.conf /etc/ntpd.conf

EXPOSE 123

ENTRYPOINT ["ntpd"]
CMD ["-d" ,"-f", "/etc/ntpd.conf", "-s"]
