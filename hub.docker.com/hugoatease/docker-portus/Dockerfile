FROM ruby:2.3

RUN apt-get update && apt-get install -y nodejs git postgresql-client --no-install-recommends

ENV RAILS_VERSION 4.2.6
RUN gem install rails --version "$RAILS_VERSION"

RUN git clone https://github.com/SUSE/Portus.git /srv/portus
WORKDIR /srv/portus

RUN bundle install

ENV RAILS_ENV production
ENV RACK_ENV production

EXPOSE 3000
CMD ["rails", "server", "-b", "0.0.0.0"]
