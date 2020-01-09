FROM gcr.io/google_containers/fluentd-elasticsearch:1.17
MAINTAINER nsidhaye 

# Install Ruby
RUN apt-get update && \
  apt-get install -y ruby ruby-dev ruby-bundler && \
  rm -rf /var/lib/apt/lists/*

