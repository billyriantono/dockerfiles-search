FROM alpine:3.7

RUN apk add --update --no-cache haproxy

# Install dockerfy
RUN apk add --update --no-cache ca-certificates curl \
 && curl -sLo /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub \
 && curl -sLO https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.28-r0/glibc-2.28-r0.apk \
 && curl -sLO https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.28-r0/glibc-bin-2.28-r0.apk \
 && curl -sL https://github.com/SocialCodeInc/dockerfy/releases/download/1.1.0/dockerfy-linux-amd64-1.1.0.tar.gz | tar -xzC /usr/bin/ \
 && apk add --no-cache glibc-2.28-r0.apk \
 && apk add --no-cache glibc-bin-2.28-r0.apk \
 && rm -f glibc-2.28-r0.apk glibc-bin-2.28-r0.apk /etc/apk/keys/sgerrand.rsa.pub

COPY haproxy.cfg /etc/haproxy/
COPY set-nameserver.sh /
RUN chmod +x /set-nameserver.sh

EXPOSE 80

ENTRYPOINT [ "/usr//bin/dockerfy", \
  "--run", "/set-nameserver.sh", "--", \
  "--start", "/sbin/syslogd", "-n", "-O", "-", "--" \
  ]

CMD ["haproxy", "-f", "/etc/haproxy/haproxy.cfg"]
