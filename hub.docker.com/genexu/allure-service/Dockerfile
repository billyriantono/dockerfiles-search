FROM openjdk:13-alpine

ARG WORKSPACE=/app

RUN apk update
RUN apk update && apk add --update nodejs nodejs-npm supervisor libressl2.7-libcrypto libstdc++ libgcc

COPY --from=genexu/watchman /usr/local/bin/watchman* /usr/local/bin/
RUN mkdir -p /usr/local/var/run/watchman && touch /usr/local/var/run/watchman/.not-empty

RUN npm install -g allure-commandline

WORKDIR $WORKSPACE
RUN mkdir allure-results

COPY ./supervisord.conf /etc/supervisord.conf

RUN watchman -- trigger $WORKSPACE/allure-results 'allure-autoload' -- supervisorctl restart allure-autoload

EXPOSE 80

CMD supervisord -c /etc/supervisord.conf

