FROM alpine:3.2

MAINTAINER alex <alexwhen@gmail.com>

ADD ./ /

RUN apk add --update bash curl py-pip supervisor jq

RUN rm -rf /var/cache/apk/*

CMD ["/bin/bash"]
