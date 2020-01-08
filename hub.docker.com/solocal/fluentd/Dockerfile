FROM fluent/fluentd:v1.7.4-debian-1.0

USER root

RUN buildDeps="sudo make gcc g++ libc-dev ruby-dev" \
 && apt-get update \
 && apt-get install -y --no-install-recommends $buildDeps \
 && sudo gem install \
        fluent-plugin-prometheus:1.6.1 \
        fluent-plugin-rewrite-tag-filter:2.2.0 \
        fluent-plugin-slack:0.6.7 \
        fluent-plugin-elasticsearch:3.5.5 \
        fluent-plugin-record-modifier:2.0.1 \
        --no-document \
 && sudo gem sources --clear-all \
 && SUDO_FORCE_REMOVE=yes \
    apt-get purge -y --auto-remove \
                  -o APT::AutoRemove::RecommendsImportant=false \
                  $buildDeps \
 && rm -rf /var/lib/apt/lists/* \
           /usr/local/lib/ruby/gems/2.6.0/cache/*.gem

USER fluent
