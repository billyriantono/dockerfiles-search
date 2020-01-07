FROM alpine:3.7

RUN apk update
RUN apk add tzdata
RUN cp /usr/share/zoneinfo/Europe/Moscow /etc/localtime
RUN echo "Europe/Moscow" > /etc/timezone
RUN apk del tzdata

RUN apk add openssh