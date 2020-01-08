FROM circleci/ruby:2.3.6-stretch-browsers
MAINTAINER Guillermo Guerrero 'wolf.fox1985@gmail.com'

RUN sudo apt-get update -qq && sudo apt-get install -y qt5-default libqt5webkit5-dev gstreamer1.0-plugins-base gstreamer1.0-tools gstreamer1.0-x nodejs
RUN sudo apt-get clean && sudo rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*