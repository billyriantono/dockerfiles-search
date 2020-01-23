FROM node:12-alpine

WORKDIR /var/www/html

COPY laravel-echo-server.example.json laravel-echo-server.json

RUN yarn global add laravel-echo-server@1.6.0

CMD ["laravel-echo-server", "start"]
