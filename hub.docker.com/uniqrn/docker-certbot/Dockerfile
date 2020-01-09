FROM certbot/dns-google
LABEL maintainer "unicorn research Ltd"

RUN apk update \
  && apk add --no-cache git openssh

WORKDIR /root
ENTRYPOINT [ "/usr/sbin/crond" ]
CMD [ "-f" ]
