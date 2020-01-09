FROM alpine

ARG REDMINE_VERSION=3.3.2
ARG RUBY_VERSION=2.3.3

RUN set -x && \
    echo "@testing http://nl.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories && \
    apk add --update apache2 apache2-utils bash font-ipa@testing git imagemagick libressl postgresql-dev subversion tar tzdata wget yaml-dev && \
    apk add --virtual .buildtools build-base apache2-dev curl-dev imagemagick-dev libffi-dev libressl-dev linux-headers pcre-dev readline-dev zlib-dev && \
    \
    mkdir /opt && cd /opt && \
    wget --no-check-certificate https://cache.ruby-lang.org/pub/ruby/2.3/ruby-2.3.3.tar.gz && \
    tar zxvf ruby-${RUBY_VERSION}.tar.gz && \
    rm -f ruby-${RUBY_VERSION}.tar.gz && \
    cd ruby-${RUBY_VERSION} && \
    ./configure --disable-install-doc && \
    make -j $(grep -c ^processor /proc/cpuinfo 2>/dev/null) && \
    make install && \
    cd /opt && rm -rf /opt/ruby-${RUBY_VERSION} && \
    \
    wget http://www.redmine.org/releases/redmine-${REDMINE_VERSION}.tar.gz && \
    tar zxvf redmine-${REDMINE_VERSION}.tar.gz && \
    rm -f redmine-${REDMINE_VERSION}.tar.gz && \
    mv redmine-${REDMINE_VERSION} redmine && \
    cd redmine && \
    gem install bundler --no-rdoc --no-ri && \
    (echo \
    "production:"; echo \
    "  adapter: postgresql"; echo \
    "  database: redmine"; echo \
    "  host: localhost"; echo \
    "  username: redmine"; echo \
    "  password: redmine"; echo \
    "  encoding: utf8") > config/database.yml && \
    cp config/configuration.yml.example config/configuration.yml && \
    sed -ie "s/rmagick_font_path:/rmagick_font_path: \/usr\/share\/fonts\/TTF\/ipagp.ttf/" config/configuration.yml && \
    bundle install --without development test --path vendor/bundle && \
    bundle exec rake generate_secret_token && \
    \
    gem install passenger --no-rdoc --no-ri && \
    passenger-install-apache2-module --auto --languages ruby && \
    (echo \
    "<Directory \"/opt/redmine/public\">"; echo \
    "  Require all granted"; echo \
    "</Directory>"; echo \
    "  ") > /etc/apache2/conf.d/redmine.conf && \
    passenger-install-apache2-module --snippet >> /etc/apache2/conf.d/redmine.conf && \
    echo "  " >> /etc/apache2/conf.d/redmine.conf && \
    (echo \
    "PassengerMaxPoolSize 20"; echo \
    "PassengerMaxInstancesPerApp 4"; echo \
    "PassengerPoolIdleTime 864000"; echo \
    "PassengerStatThrottleRate 10"; echo \
    "Header always unset \"X-Powered-By\""; echo \
    "Header always unset \"X-Runtime\"") >> /etc/apache2/conf.d/redmine.conf && \
    echo "  " >> /etc/apache2/conf.d/redmine.conf && \
    (echo \
    "Alias /redmine /opt/redmine/public"; echo \
    "<Location /redmine>"; echo \
    "  PassengerBaseURI /redmine"; echo \
    "  PassengerAppRoot /opt/redmine"; echo \
    "</Location>") >> /etc/apache2/conf.d/redmine.conf && \
    \
    mkdir -p /run/apache2 && \
    chown -R apache:apache /opt/redmine && \
    \
    apk del .buildtools && \
    rm -rf /var/cache/apk/*

COPY entrypoint.sh /opt/
RUN chmod 755 /opt/entrypoint.sh

CMD ["/opt/entrypoint.sh"]
