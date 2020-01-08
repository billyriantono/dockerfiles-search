FROM openjdk:8-jdk
MAINTAINER matico <mactiencong@gmail.com>

RUN apt-get update && \
curl -sL https://deb.nodesource.com/setup_8.x | bash && \
apt-get install -y nodejs && \
npm -g install eslint babel-eslint && \
npm -g install eslint-config-airbnb eslint-plugin-jsx-a11y eslint-plugin-react eslint-plugin-import && \
npm -g i eslint-plugin-jest