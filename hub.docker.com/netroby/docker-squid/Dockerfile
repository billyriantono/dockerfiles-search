FROM alpine
RUN apk add -U squid
ADD squid.conf /etc/squid/squid.conf
CMD ["squid", "-NCdl"]
