FROM ruby:2.5.3
RUN gem install -N rails:5.2.2
RUN apt-get -y update && \
    apt-get -y install \
      gifsicle \
      jhead \
      jpegoptim \
      nodejs \
      optipng
