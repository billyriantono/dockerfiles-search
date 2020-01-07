FROM ruby:alpine

RUN gem install s3_website -v 3.1.0

RUN apk update
RUN apk add openjdk7-jre

VOLUME ["/website", "/config"]

WORKDIR /website

ENTRYPOINT ["s3_website"]

CMD ["--help"]
