FROM ruby:2.5.1
MAINTAINER Jian-Long Huang <huang@jianlong.org>
EXPOSE 4567
RUN apt-get -qq update && apt-get install -y nodejs apache2 && apt-get clean
RUN mkdir /app
WORKDIR /app
COPY ./slate /app
RUN bundle install
CMD bash -c 'bundle exec middleman build --clean && cp -r build/* /var/www/html/ && apachectl -D FOREGROUND'
