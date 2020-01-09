# Base image:
FROM ruby:2.3-slim
MAINTAINER Julio Lustosa "contato@juliolustosa.com.br"

RUN apt-get update && apt-get install -y \
  build-essential \
  sqlite3 \
  libsqlite3-dev

# Install Gem mailcatcher for test e-mails
RUN gem install mailcatcher

# smtp port
EXPOSE 1025

# webserver port
EXPOSE 1080

# Start mailcatcher
CMD ["mailcatcher", "-f", "--ip=0.0.0.0"]
