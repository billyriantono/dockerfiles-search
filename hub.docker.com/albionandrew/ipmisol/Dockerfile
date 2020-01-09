FROM alpine:latest
MAINTAINER Andrew Chandler <andrew+dockerhub@phoe.be>

ENV USERNAME=ADMIN
ENV PASSWORD=ADMIN
ENV PREFIX=ipmi-

RUN apk add --update --no-cache ipmitool
ADD ./ipmiscript.sh /ipmiscript.sh
ENTRYPOINT ["/ipmiscript.sh"]
CMD []
