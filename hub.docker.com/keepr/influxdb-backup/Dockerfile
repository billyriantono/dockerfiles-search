FROM influxdb:1.3.7-alpine

RUN apk update && apk add curl python ca-certificates && rm -rf /var/cache/apk/*

RUN cd /usr/local/bin; curl https://storage.googleapis.com/pub/gsutil.tar.gz| tar xfz -
