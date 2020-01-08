FROM breauxaj/alpine:latest

COPY Gemfile /Gemfile

RUN apk add ruby shadow less \
  && gem install bundler \
  && bundle install \
  && rm -rf /var/cache/apk/* \
  && mkdir -p /etc/puppet

CMD ["sh"]

LABEL org.opencontainers.image.vendor="Breaux Heavy Industries" \
	org.opencontainers.image.url="https://breaux.io" \
	org.opencontainers.image.title="Puppet" \
	org.opencontainers.image.description="Puppet 6.x, strictly intended for running tests" \
	org.opencontainers.image.version="v0.0.1" \
	org.opencontainers.image.documentation="https://docs.breaux.io"