FROM alpine:3.2

RUN apk --update add bash nodejs
RUN npm install -g elasticdump

ENTRYPOINT ["/usr/bin/elasticdump"]
