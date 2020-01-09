
  FROM debian:stretch-20181226
  CMD ["bash"]
  ARG PACT_RUBY_VERSION=1.63.0
  WORKDIR /pact-ruby
  RUN PACT_RUBY_VERSION=1.63.0 apt-get update \
  && apt-get install -y curl \
  && curl -L -O https://github.com/pact-foundation/pact-ruby-standalone/releases/download/v${PACT_RUBY_VERSION}/pact-${PACT_RUBY_VERSION}-linux-x86_64.tar.gz \
  && tar -xf pact-${PACT_RUBY_VERSION}-linux-x86_64.tar.gz \
  && rm pact-${PACT_RUBY_VERSION}-linux-x86_64.tar.gz \
  && apt-get purge -y curl && apt-get -y --purge autoremove \
  && rm -rf /var/lib/apt/lists/* /etc/apt/sources.list.d/*
  ENV PATH=/pact-ruby/pact/bin/:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
  EXPOSE 8080
