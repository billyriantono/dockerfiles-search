FROM golang:1.10-alpine

RUN apk add --no-cache \
        git \
        curl

RUN curl https://raw.githubusercontent.com/golang/dep/master/install.sh | sh

COPY docker-entrypoint.sh /
RUN chmod a+x /docker-entrypoint.sh

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["ensure"]
