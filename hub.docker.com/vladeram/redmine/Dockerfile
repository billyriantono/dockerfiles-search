FROM redmine:4.0.0

MAINTAINER vladeram

WORKDIR /usr/src/redmine

COPY plugins /usr/src/redmine/plugins/
COPY getmail.rb /usr/src/redmine/config/initializers/getmail.rb

RUN gem install rufus-scheduler \
    && echo "gem 'rufus-scheduler'" >> Gemfile \
    && bundle install --no-deployment