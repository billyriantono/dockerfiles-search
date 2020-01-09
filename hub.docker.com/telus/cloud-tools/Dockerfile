#####
FROM alpine/helm:2.12.3 as helm
FROM chef/inspec:3.6.10 as inspec
FROM telus/cloud-tools:latest
MAINTAINER "telus/dockerfiles"

# paths #
ENV BINPATH "/usr/local/bin"

# install #
RUN apk add --update \
  "build-base" \
  "nodejs" \
  "npm" \
  "ruby" \
  "ruby-dev" \
  "ruby-etc" \
  ;
RUN gem install --no-document "io-console" ;
RUN gem install --no-document --version "3.6.6" "inspec" ;
RUN gcloud components install kubectl ;
COPY --from=helm /usr/bin/helm ${BINPATH}/helm

# clean #
RUN apk del \
  "build-base" \
  "ruby-dev" \
  ;
RUN rm -rf /var/cache/apk/* ;

# version #
RUN helm version --client ;
RUN inspec version ;
