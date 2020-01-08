FROM node:6-alpine
MAINTAINER Conmio developers
RUN apk --no-cache update && \
    apk --no-cache add less bash make curl openssl su-exec

COPY script/entrypoint.sh /usr/local/bin/entrypoint.sh
RUN chmod 755 /usr/local/bin/entrypoint.sh

WORKDIR /app

ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
