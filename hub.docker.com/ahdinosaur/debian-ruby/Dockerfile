FROM debian:wheezy

MAINTAINER Michael Williams dinosaur@riseup.net

ADD etc/apt/sources.list.d/jessie.list /etc/apt/sources.list.d/jessie.list
ADD etc/apt/preferences.d/jessie.pref /etc/apt/preferences.d/jessie.pref
ADD etc/apt/preferences.d/ruby.pref /etc/apt/preferences.d/ruby.pref

RUN apt-get update
RUN apt-get install -y ruby2.0 bundler
