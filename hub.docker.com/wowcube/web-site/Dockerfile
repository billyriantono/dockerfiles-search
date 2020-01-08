# light weight node image
FROM node:10.18.0-alpine3.10

RUN mkdir /website
WORKDIR /website

COPY ./*.js*      /website/
COPY ./*.lock     /website/

COPY ./assets     /website/assets
COPY ./components /website/components
COPY ./layouts    /website/layouts
COPY ./middleware /website/middleware
COPY ./pages      /website/pages
COPY ./plugins    /website/plugins
COPY ./static     /website/static
COPY ./store      /website/store
COPY ./vendor     /website/vendor
COPY ./lang       /website/lang

ARG WOW_LANG
ENV WOW_LANG $WOW_LANG
ARG BASE_URL
ENV BASE_URL $BASE_URL
RUN cd /website && ls -all && yarn install && yarn run build

# needs for nuxt, it makes visible webserver outside the container
ENV HOST 0.0.0.0

CMD ["yarn", "start"]

EXPOSE 3000
