FROM node:8.15-alpine

RUN mkdir /bld
COPY ./*.js*  /bld/
COPY ./*.lock /bld/
COPY ./src    /bld/src
COPY ./public /bld/public
RUN apk add --no-cache git
RUN cd /bld && yarn install && yarn run build

FROM nginx:1.11

COPY          ./nginx    /etc/nginx
COPY --from=0  /bld/dist /www

EXPOSE 8086
