# Base from Google App Engine Image
FROM l.gcr.io/google/ruby:latest
MAINTAINER Julio Lustosa "contato@juliolustosa.com.br"

# Install dependencies
RUN apt-get update -qq && apt-get install -y \
  build-essential \
  libpq-dev \
  nodejs \
  openssh-client \
  git-core \
  curl \
  wget \
  mysql-client \
  postgresql-client

# Install Gems
RUN gem install bundler
RUN gem install rack

# Set an environment variable where the Rails app is installed to inside of Docker image:
ENV APP_HOME /app

# Set working directory, where the commands will be ran:
WORKDIR /app

# Copy Scripts
RUN mkdir -p /scripts
COPY ./docker-scripts /scripts

# Copy application files and install
ONBUILD COPY . /app/
ONBUILD RUN ruby /scripts/config.rb

EXPOSE 8080

CMD ["ruby", "/scripts/config.rb"]

# Default container command invokes rackup to start the server.
ENTRYPOINT ["bundle", "exec", "rackup", "--port=8080"]