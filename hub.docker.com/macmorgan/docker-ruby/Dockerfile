FROM dockerfile/ubuntu
MAINTAINER Mac Morgan <mac@macmorgan.com>

# Install Ruby.
RUN \
  apt-get update && \
  apt-get install -y build-essential ruby ruby-dev ruby-bundler mysql-client libmysqlclient-dev && \
  rm -rf /var/lib/apt/lists/*

# Define working directory.
WORKDIR /data

# Define default command.
CMD ["bash"]
