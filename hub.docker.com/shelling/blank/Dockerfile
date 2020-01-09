FROM ubuntu:18.04

RUN apt-get update -qq && apt-get install -y aptitude git libpq-dev curl vim bash-completion htop postgresql-client nodejs npm gnupg2

RUN curl -sSL https://rvm.io/mpapis.asc | gpg2 --import -
RUN gpg2 --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
RUN \curl -sSL https://get.rvm.io | bash -s stable
RUN /bin/bash -l -c "rvm install 2.4.1"
RUN /bin/bash -l -c "gem install bundler -v 1.16.1 --no-ri --no-rdoc"

ENV APP_ROOT /app

RUN mkdir $APP_ROOT
WORKDIR $APP_ROOT
ADD . $APP_ROOT
RUN /bin/bash -l -c "bundle install"

EXPOSE 3000
CMD ["/bin/bash", "-l", "-c", "bundle exec rails server -b 0.0.0.0"]
