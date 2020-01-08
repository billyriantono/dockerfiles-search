FROM ruby:2.3.5
MAINTAINER Marc Wickenden <marc@4armed.com>

RUN apt-get update && apt-get install -y build-essential zip libmysqlclient-dev libpq-dev libaio1 imagemagick libmagickwand-dev && rm -rf /var/lib/apt/lists/*

ADD instantclient-basiclite-linux.x64-11.2.0.4.0.zip /
ADD instantclient-sdk-linux.x64-11.2.0.4.0.zip /
ADD instantclient-sqlplus-linux.x64-11.2.0.4.0.zip /

RUN mkdir -p /opt/oracle && cd /opt/oracle && unzip /instantclient-basiclite-linux.x64-11.2.0.4.0.zip && unzip /instantclient-sdk-linux.x64-11.2.0.4.0.zip && unzip /instantclient-sqlplus-linux.x64-11.2.0.4.0.zip
RUN cd /opt/oracle/instantclient_11_2 && ln -s libclntsh.so.11.1 libclntsh.so
ADD oracle-lib.conf /etc/ld.so.conf.d/
RUN ldconfig && echo 'export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/opt/oracle/instantclient_11_2' >> /etc/bash.bashrc

RUN mkdir /remote_gems
RUN echo 'gem: --no-rdoc --no-ri' >> $HOME/.gemrc && \
    gem install bundler && \
    bundle config path /remote_gems

ENV RAILS_ENV production
ENV RACK_ENV production

WORKDIR /app
ONBUILD ENV LD_LIBRARY_PATH /opt/oracle/instantclient_11_2
ONBUILD ADD Gemfile /app/Gemfile
ONBUILD ADD Gemfile.lock /app/Gemfile.lock
ONBUILD RUN bundle install --deployment --without development test
ONBUILD ADD . /app

CMD bundle exec unicorn -c config/unicorn.rb
