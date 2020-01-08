FROM ruby:2.3.0

RUN apt-get -y update
RUN apt-get -y install qt5-default libqt5webkit5-dev \
	       gstreamer1.0-plugins-base gstreamer1.0-tools gstreamer1.0-x \
	       xvfb

RUN gem install jekyll capybara-webkit

