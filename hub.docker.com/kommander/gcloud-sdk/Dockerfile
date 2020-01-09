FROM google/cloud-sdk:265.0.0-alpine

# Install Ruby and clean the installer cache
RUN apk --update add --no-cache ruby ruby-json ruby-dev build-base && \
    gem install bigdecimal slack-ruby-client --no-rdoc --no-ri && \
    apk del build-base

# Install kubectl
RUN gcloud components install kubectl
