FROM alpine:latest
ENV API_URL "http://api.jalapenos.eu"

RUN apk add --update bash nodejs npm gettext lighttpd

COPY ./package.json /var/www/package.json
WORKDIR /var/www
RUN npm install

RUN addgroup node && \
    adduser -D -s /bin/bash -h /var/www -G node node

COPY . /var/www

RUN /var/www/make-env.sh
RUN npm run build

ENTRYPOINT ["/usr/bin/env", "bash"]
CMD ["docker-entry.sh"]

EXPOSE 8080