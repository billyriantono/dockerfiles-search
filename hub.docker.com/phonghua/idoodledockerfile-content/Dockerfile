FROM ruby:2.6.3-alpine3.10

# params
ENV SITE_CODE=TEST
ENV PROFILE=TEST
ENV ELASTIC_SEARCH_USER=
ENV ELASTIC_SEARCH_PWD=

# setup fluent
RUN apk add --no-cache --virtual .build-deps \
                build-base \
        && echo 'gem: --no-document' >> /etc/gemrc \
        && gem install oj \
        && gem install json \
        && gem install async-http \
        && gem install fluentd \
        && gem install bigdecimal \
        && fluentd --setup ./fluent \
        && apk del .build-deps \
        && rm -rf /tmp/* /var/tmp/* /usr/lib/ruby/gems/*/cache/*.gem

# copy configuration
COPY ["fluent.conf", "/fluent/"]

# install plugins
RUN fluent-gem install \
        fluent-plugin-grok-parser \
        fluent-plugin-concat \
        fluent-plugin-elasticsearch

# conatiners entry point
ENTRYPOINT ["fluentd", "-c",  "./fluent/fluent.conf"]