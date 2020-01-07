FROM cnosuke/ruby22-base
MAINTAINER cnosuke

RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y \
  imagemagick \
  libmagickwand-dev \
  memcached

RUN git clone https://github.com/negipo/lgtm.git /app
RUN echo "gem 'unicorn'" >> /app/Gemfile
RUN echo "gem 'dotenv'" >> /app/Gemfile
RUN cd /app && bundle install

ADD env /app/.env
ADD run.sh /app/run.sh
ADD unicorn.rb /app/unicorn.rb
ADD memcached.conf /etc/memcached.conf
RUN mkdir -p /app/tmp /app/log

EXPOSE 8080
CMD ["/app/run.sh"]
