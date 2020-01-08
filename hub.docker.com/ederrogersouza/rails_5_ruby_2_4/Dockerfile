FROM ruby:2.4

RUN apt-get update
RUN apt-get install -y ruby-dev
RUN apt-get install -y autoconf bison build-essential libssl-dev libyaml-dev
RUN apt-get install -y libreadline6-dev zlib1g-dev libncurses5-dev libffi-dev libgdbm3 libgdbm-dev
RUN gem update --system
RUN gem install bundler
RUN gem install rails -v 5.0.1
RUN apt-get install -y nodejs --no-install-recommends && rm -rf /var/lib/apt/lists/*

RUN gem install rake
