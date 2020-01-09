FROM alpine

RUN apk --no-cache add \
    nodejs \
    nodejs-npm \
    yarn

WORKDIR /app
ENTRYPOINT ["yarn"]
CMD ["help"]
