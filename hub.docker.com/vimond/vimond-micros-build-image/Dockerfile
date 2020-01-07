FROM circleci/openjdk:8-jdk

# Install nodejs and npm
RUN curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
RUN sudo apt-get update && \
  sudo apt-get install -y \
  nodejs \
  python-pip \
  python-sphinx \
  build-essential \
  && sudo rm -rf /var/lib/apt/lists/*

# Necessary tools for compiling documentation
RUN sudo npm install -g less
RUN sudo pip install -U urllib3

