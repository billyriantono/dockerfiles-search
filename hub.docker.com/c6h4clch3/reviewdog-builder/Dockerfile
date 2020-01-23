FROM alpine:latest

RUN URL=https://raw.githubusercontent.com/reviewdog/reviewdog/master/install.sh && \
      wget -O - -q ${URL} | sh -s
RUN apk add --update git
