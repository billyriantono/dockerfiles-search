FROM ruby:2.4.3-slim

ENV TERRAFORM_LANDSCAPE_VERSION=0.2.1

RUN gem install --no-document --no-ri terraform_landscape:${TERRAFORM_LANDSCAPE_VERSION}

ENTRYPOINT ["landscape"]
