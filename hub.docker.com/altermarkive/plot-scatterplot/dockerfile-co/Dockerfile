# Pull base image.
FROM ubuntu:16.04

# Install.
RUN \
  sed -i 's/# \(.*multiverse$\)/\1/g' /etc/apt/sources.list && \
  apt-get update && \
  apt-get install -y wget && \
  wget https://packages.erlang-solutions.com/erlang-solutions_1.0_all.deb && dpkg -i erlang-solutions_1.0_all.deb && \
  apt-get update && \
  apt-get -y upgrade && \
  apt-get install -y curl inotify-tools && \
  apt-get install -y build-essential && \
  apt-get install -y nodejs && \
  apt-get install -y npm && \
  ln -s /usr/bin/nodejs /usr/bin/node && \
  apt-get install -y esl-erlang && \
  apt-get install -y elixir && \
  apt-get install -y git && \
  npm install -g gulp-cli && \
  rm -rf /var/lib/apt/lists/*

# Add files.
# ADD root/.bashrc /root/.bashrc

# Define default command.
CMD ["bash"]