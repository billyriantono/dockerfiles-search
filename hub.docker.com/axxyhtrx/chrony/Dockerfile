FROM alpine:latest

RUN apk add --no-cache chrony
COPY ./crony.conf /etc/chrony/chrony.conf
EXPOSE 123/udp

ENTRYPOINT [ "/usr/sbin/chronyd", "-d", "-s"]
