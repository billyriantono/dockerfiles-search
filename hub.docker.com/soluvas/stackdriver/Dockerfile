FROM ubuntu:xenial

MAINTAINER Hendy Irawan <hendy@hendyirawan.com>

# Install curl
RUN apt-get update && apt-get install -y curl

# Prepare Stackdriver installation
RUN curl -s -S -f -o /etc/apt/sources.list.d/stackdriver.list "https://repo.stackdriver.com/xenial.list" \
  && (curl -s -f https://app.stackdriver.com/RPM-GPG-KEY-stackdriver | apt-key add -) \
  && apt-get update

# Install the agent package, without prompting for an API key.
ENTRYPOINT ["apt-get"]
CMD ["-y", "-q", "install", "stackdriver-agent"]
