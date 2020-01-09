FROM fluent/fluentd:v1.3-debian-1
LABEL maintainer="ROY XU <qqbuby@gmail.com>"

USER root

# Do not split this into multiple RUN!
# Docker creates a layer for every RUN-Statement
# therefore an 'apt-get purge' has no effect
RUN apt-get update \
 && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
            ca-certificates \
            ruby \
 && buildDeps=" \
      make gcc g++ libc-dev \
      ruby-dev \
      wget bzip2 gnupg dirmngr \
    " \
 && apt-get install -y --no-install-recommends $buildDeps \
 && echo 'gem: --no-document' >> /etc/gemrc \
 && gem install fluent-plugin-elasticsearch -v '~> 3.2.0' \
 && gem install fluent-plugin-rewrite-tag-filter -v '~> 2.1.1' \
 && gem install fluent-plugin-systemd -v '~> 1.0.2' \
 && gem install fluent-plugin-multi-format-parser -v '~> 1.0.0' \
 && gem install fluent-plugin-kubernetes_metadata_filter -v '~> 2.1.6' \
 && gem install fluent-plugin-prometheus -v '~> 1.3.0' \
 && apt-get purge -y --auto-remove \
                  -o APT::AutoRemove::RecommendsImportant=false \
                  $buildDeps \
 && rm -rf /var/lib/apt/lists/* \
 && rm -rf /tmp/* /var/tmp/* /usr/lib/ruby/gems/*/cache/*.gem

COPY ./fluent.root.conf /etc/fluent/fluent.conf
COPY ./run.sh /run.sh

CMD [ "/bin/sh", "-c", "/run.sh $FLUENTD_ARGS" ]

#USER fluent
