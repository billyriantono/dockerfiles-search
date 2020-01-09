FROM nginx:1.16.0-alpine

LABEL maintainer "NeverBehave <gayhub@never.pet>"
ARG ARCH=amd64
RUN apk -U --no-cache add bash \
    && rm -f /bin/sh \
    && ln -s /bin/bash /bin/sh
RUN apk -U --no-cache add curl ca-certificates tar \
    && mkdir -p /etc/confd \
    && curl -sLf https://github.com/kelseyhightower/confd/releases/download/v0.16.0/confd-0.16.0-linux-${ARCH} > /usr/bin/confd \
    && chmod +x /usr/bin/confd

COPY templates /etc/confd/templates/
COPY conf.d /etc/confd/conf.d/
COPY nginx-proxy /usr/bin/

RUN chmod +x /usr/bin/nginx-proxy

CMD ["/bin/bash"]