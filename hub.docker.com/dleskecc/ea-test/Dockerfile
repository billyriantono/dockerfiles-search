FROM alpine:latest
LABEL maintainer="Drew Leske <drew.leske@computecanada.ca>"

# install ElastAlert
RUN apk update && apk add gcc py-pip python2-dev libffi-dev musl-dev openssl-dev libmagic
RUN pip install elastalert

# remove build tools
RUN apk del gcc libffi-dev musl-dev openssl-dev python2-dev
RUN rm -Rf /var/cache/apk
