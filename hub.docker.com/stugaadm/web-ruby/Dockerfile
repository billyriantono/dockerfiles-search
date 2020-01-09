FROM stugaadm/web-base

MAINTAINER StugA-Admins <stuga-adm@fb3.uni-bremen.de>

ENV GEM_HOME $DATA/gems
ENV PATH $GEM_HOME/bin:$PATH

ENV BUNDLER_VERSION 1.10.5

RUN apk --update add ruby ruby-dev sqlite-dev nodejs gcc libc-dev zlib-dev libxml2-dev libxslt-dev make libffi-dev

RUN chown -R $USER_NAME:$USER_NAME $DATA

USER $USER_NAME

RUN echo 'gem: --no-rdoc --no-ri' >> "$DATA/.gemrc"

RUN mkdir -p $GEM_HOME
RUN ls -la $GEM_HOME
RUN gem install tzinfo-data bundler:"$BUNDLER_VERSION" \
        && bundle config --global path "$GEM_HOME" \
        && bundle config --global bin "$GEM_HOME/bin" \
        && bundle config --global build.nokogiri --use-system-libraries

ONBUILD USER root
