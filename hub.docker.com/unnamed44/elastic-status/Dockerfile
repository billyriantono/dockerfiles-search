FROM alpine

RUN apk add --no-cache curl jq bash

COPY elasticsearch-status /usr/bin/elasticsearch-status

CMD [ "elasticsearch-status" ]
