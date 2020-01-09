FROM ruby:alpine as build

RUN apk add -U alpine-sdk icu-dev && \
    gem install gollum github-markdown

FROM ruby:alpine

ARG BUILD_DATE=''
ARG VCS_REF=''

LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.name="Gollum" \
      org.label-schema.description="Docker packaged Gollum Wiki" \
      org.label-schema.url="https://github.com/kns-it/docker-gollum" \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="https://github.com/kns-it/docker-gollum" \
      org.label-schema.vendor="KNS" \
      org.label-schema.schema-version="1.0" \
      maintainer="sebastian.kurfer@kns-it.de"

RUN apk add -U --no-cache git icu

COPY --from=build /usr/local/bundle/ /usr/local/bundle/

EXPOSE 4567

WORKDIR /work

ENTRYPOINT ["/usr/local/bundle/bin/gollum"]
