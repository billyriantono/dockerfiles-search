FROM mhart/alpine-node:latest
LABEL maintainer="Dan Jellesma"

ARG VCS_REF
ARG BUILD_DATE

RUN npm i speed-test -g

RUN mkdir /public
WORKDIR /public

CMD ["speed-test"]
