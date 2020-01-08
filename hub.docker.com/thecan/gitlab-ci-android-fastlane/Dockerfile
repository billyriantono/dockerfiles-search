#
# GitLab CI: Android with Fastlane
#
#

FROM thecan/gitlab-ci-android
MAINTAINER Daniel Cerny <daniel.troll.cerny@gmail.com>

RUN mkdir $HOME/utils \
	&& curl -L https://bitbucket.org/iBotPeaches/apktool/downloads/apktool_2.3.4.jar -o $HOME/utils/apktool.jar
RUN apt-get update \
    && apt-get install \
        ruby-dev -y \
    	build-essential -y
RUN curl -L https://rubygems.org/rubygems/rubygems-2.7.7.tgz -o ruby.tgz \
    && tar xvfz ruby.tgz \
    && rm ruby.tgz \
    && cd rubygems-2.7.7 \
    && ruby setup.rb \
    && gem install fastlane
