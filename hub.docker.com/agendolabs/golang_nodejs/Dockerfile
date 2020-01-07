FROM golang:1.6.2-alpine
RUN apk add --no-cache nodejs git 
RUN git clone https://github.com/etsy/statsd.git

WORKDIR /go

#ENTRYPOINT ["node", "/statsd/stats.js", "/statsd/exampleConfig.js"]