FROM ubuntu:bionic

MAINTAINER codeculture <development@codeculture.de>

RUN apt-get update && apt-get install -y sudo curl && \
    curl -sL https://deb.nodesource.com/setup_10.x | bash - && \
    curl -sL https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list && \
    apt-get update && \
    apt-get install -y jq yarn nodejs wget ruby-dev gcc g++ make python build-essential openjdk-8-jdk-headless git && \
    gem install fastlane

RUN npm install -g turtle-cli gulp-cli expo-cli --unsafe-perm=true --allow-root
