FROM circleci/android:api-27-ndk

USER root

# INSTALL NODE
ENV NODE_VERSION=8.10.0

RUN apt-get update
RUN apt-get -y install curl gnupg
RUN curl -sL https://deb.nodesource.com/setup_8.x  | bash -
RUN apt-get -y install nodejs

# INSTALL RUBY
RUN apt-get -y install ruby-full
RUN gem install bundler
