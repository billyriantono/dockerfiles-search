FROM alpine

LABEL maintainer="Ghostry <ghostry.green@gmail.com>"

RUN apk add --no-cache curl openssl socat; \
    curl https://get.acme.sh |sh;\
    ln /root/.acme.sh/acme.sh /bin/acme

WORKDIR /

VOLUME ["/data"]

CMD ["acme"]