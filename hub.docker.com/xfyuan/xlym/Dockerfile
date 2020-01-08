FROM ruby:2.2

# ===================================
# apt package update and installation
# ===================================
RUN apt-get update -qq && apt-get install -y build-essential
# for nokogiri
RUN apt-get install -y libxml2-dev libxslt1-dev
# for capybara-webkit
RUN apt-get install -y libqt4-webkit libqt4-dev xvfb
# for js runtime
RUN apt-get install -y nodejs
# clean apt package cache
RUN rm -rf /var/lib/apt/lists/*


# ==============================
# install bundler and setting it
# ==============================
RUN gem install bundler
ENV BUNDLE_PATH /rubygems

