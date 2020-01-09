FROM node:10-alpine

RUN apk add --no-cache su-exec

RUN npm install -g tiddlywiki

# Setup wiki volume
VOLUME /var/lib/tiddlywiki
WORKDIR /var/lib/tiddlywiki

# Add init-and-run script
ADD tiddlyweb_host /tiddlyweb_host_template
ADD init-and-run-wiki /usr/local/bin/init-and-run-wiki

ENV PUID=1000 PGID=1000

HEALTHCHECK --interval=1m --timeout=10s \
    CMD nc -z localhost 8080 || exit 1

# Meta
CMD ["/usr/local/bin/init-and-run-wiki"]
EXPOSE 8080
