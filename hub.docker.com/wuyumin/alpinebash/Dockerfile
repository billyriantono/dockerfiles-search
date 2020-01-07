FROM wuyumin/base

LABEL maintainer="Yumin Wu"

RUN apk update && apk upgrade \
  && apk add bash \
  && rm -rf /var/cache/apk/* /tmp/*

CMD ["/bin/bash","-l"]
