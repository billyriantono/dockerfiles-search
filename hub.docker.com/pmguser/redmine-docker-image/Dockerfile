FROM redmine:3.4.2
ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
    && apt-get install -y supervisor \
    && mkdir -p /var/log/supervisor \
    && apt-get install -y vim \
    && apt-get install -y sendmail \
    && apt-get install -y build-essential patch \
    && apt-get install -y cron \
    && touch /var/log/redmine-fetch.log \
    && chown redmine /var/log/redmine-fetch.log \
    && chmod 664 /var/log/redmine-fetch.log \
    && gem install nokogiri -v '1.6.8' \
    && apt-get install -y libmysqlclient-dev \
    && apt-get install -y libmagickwand-dev imagemagick

COPY config/supervisord.conf /etc/supervisor/supervisord.conf
COPY config/scripts/hostname-config.sh /usr/local/bin/
ENV TZ=America/Chicago

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime \
    && echo $TZ > /etc/timezone \
    && rm -rf /usr/local/bundle/* \
    && chmod +x /usr/local/bin/hostname-config.sh \
    && rm /usr/src/redmine/Gemfile.lock

COPY config/Gemfile /usr/src/redmine
COPY config/docker-entrypoint.sh /docker-entrypoint.sh
RUN bundle install

CMD ["/usr/bin/supervisord"]
