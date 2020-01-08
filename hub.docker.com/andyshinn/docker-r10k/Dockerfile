FROM alpine:3.6
RUN apk add --no-cache ruby ruby-json
RUN gem install --no-document -v 2.5.5 r10k
ENTRYPOINT ["r10k"]
