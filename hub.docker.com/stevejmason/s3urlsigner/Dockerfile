FROM ruby:2.2.0
MAINTAINER Stephen J. Mason <hi@stephenmason.me>

# Usual update
RUN apt-get update

# Set working DIR 
WORKDIR /usr/local/s3urlsigner

# Add Gemfile for better caching
COPY Gemfile /usr/local/s3urlsigner/
COPY Gemfile.lock /usr/local/s3urlsigner/
RUN bundle install

# Copy accress s3urlsigner source
COPY . /usr/local/s3urlsigner

# Expose service port
EXPOSE 8080

# Set entrypoint as unicorn through bundler
ENTRYPOINT ["/usr/local/s3urlsigner/docker/start.sh"]




