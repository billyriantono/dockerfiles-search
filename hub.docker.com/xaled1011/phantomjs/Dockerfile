FROM ubuntu:16.04

RUN \
  apt-get update && \
  apt-get -y upgrade && \
  apt-get install -y phantomjs && \
  rm -rf /var/lib/apt/lists/*


# Define default command.
CMD ["bash"]
