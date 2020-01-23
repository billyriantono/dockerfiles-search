FROM mhart/alpine-node:10.3.0 AS local

RUN apk update && apk upgrade && apk add git && apk add python && apk add make && apk add g++ && npm i -g yarn

ENV APP_HOME /usr/src/app
VOLUME ${APP_HOME}
EXPOSE 3000
EXPOSE 4000
WORKDIR $APP_HOME
CMD ["yarn", "run", "start:dev"]

FROM mhart/alpine-node:10.3.0 AS stage
RUN apk update && apk upgrade && apk add git && apk add python && apk add make && apk add g++ && npm i -g yarn
ENV APP_HOME /usr/src/app
EXPOSE 3000
EXPOSE 4000
WORKDIR $APP_HOME
ADD . $APP_HOME/
RUN yarn
CMD ["yarn", "run", "start:dev"]

FROM mhart/alpine-node:10.3.0 AS test

RUN apk update && apk upgrade && apk add git && apk add python && apk add make && apk add g++ && npm i -g yarn

ENV APP_HOME /usr/src/app

EXPOSE 3000
EXPOSE 4000
WORKDIR $APP_HOME
ADD . $APP_HOME/
RUN yarn --production=false


FROM mhart/alpine-node:10.3.0 AS production

RUN apk update && apk upgrade && apk add git && apk add python && apk add make && apk add g++ && npm i -g yarn
COPY --from=test /usr/src/app /usr/src/app
EXPOSE 3000
EXPOSE 4000
WORKDIR /usr/src/app
RUN yarn prestart:prod
CMD ["yarn", "start:prod"]