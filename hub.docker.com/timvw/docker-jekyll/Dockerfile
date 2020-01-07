FROM ubuntu:latest
MAINTAINER Tim Van Wassenhove <tim@icteam.be>

RUN apt-get update \
  && apt-get install bash curl vim ruby ruby-dev jekyll nodejs python git gcc make build-essential patch zlib1g-dev liblzma-dev -y \
  && apt-get clean \
  && gem install bundler \
  && gem update --system \
  && mkdir /opt/website \
  && printf "source 'https://rubygems.org'\ngem 'github-pages', group: :jekyll_plugins" > /opt/website/Gemfile \
  && bundle config --global silence_root_warning 1
#  && bundle install

WORKDIR /opt/website

RUN bundle install

EXPOSE 4000

VOLUME ["/opt/website"]

#CMD ["/usr/bin/jekyll", "serve", "-incremental"]
CMD ["/bin/bash"]
