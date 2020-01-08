# uses the circle image + installs some extra packages so that the capybara-webkit gem installs
# image is then pushed to cloud.docker.com from where its fetched by circleci...
FROM circleci/ruby:2.6.3-node-browsers

RUN sudo apt-get update && sudo apt-get install software-properties-common gcc g++ make qt5-default libqt5webkit5-dev ruby-dev zlib1g-dev phantomjs
