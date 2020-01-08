FROM circleci/ruby:2.6.3-node

RUN sudo apt-get update -qq && \
    sudo apt-get install -y ghostscript libmagickwand-dev --fix-missing --no-install-recommends && \
    sudo apt-get clean && \
    sudo rm -rf /var/lib/apt/lists/*
