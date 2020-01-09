FROM node:alpine

RUN apk add --no-cache bash tini

WORKDIR /var/www

ENTRYPOINT ["/sbin/tini", "--", "npm", "run"]

CMD ["watch"]