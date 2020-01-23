FROM python:3.6.0

MAINTAINER CubYard.com <cubyard.com@gmail.com>

SHELL ["/bin/bash", "-c"]

ENV RAILS_VERSION 5.0.1
ENV RUBY_VERSION 2.3.1

RUN apt-get update \
  && apt-get install -y build-essential postgresql postgresql-contrib libpq-dev zip unzip python-dev git \
  && git clone https://github.com/rbenv/rbenv.git ~/.rbenv \
  && echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc \
  && echo 'eval "$(rbenv init -)"' >> ~/.bashrc \
  && source ~/.bashrc \
  && git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build \
  && rbenv install $RUBY_VERSION \
  && rbenv global $RUBY_VERSION \
  && gem install rails --version=$RAILS_VERSION \
  && gem install pg json byebug nokogiri ffi

RUN curl "https://s3.amazonaws.com/aws-cli/awscli-bundle.zip" -o "awscli-bundle.zip" \
  && unzip awscli-bundle.zip \
  && ./awscli-bundle/install -i /usr/local/aws -b /usr/local/bin/aws

RUN pip install --upgrade --user awsebcli

ENV PATH "$PATH:~/.local/bin/"

RUN sed -i 's/peer/trust/g' /etc/postgresql/9.*/main/pg_hba.conf