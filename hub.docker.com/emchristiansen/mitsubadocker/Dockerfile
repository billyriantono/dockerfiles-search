FROM ubuntu:14.04

MAINTAINER Eric Christiansen <ericmartinchristiansen@gmail.com>

RUN sudo apt-get update && sudo apt-get install -y wget python-numpy

RUN wget http://www.mitsuba-renderer.org/releases/current/trusty/collada-dom_2.4.0-1_amd64.deb
# This two-step install is a hack to automatically install the dependencies.
RUN sudo dpkg -i collada-dom_2.4.0-1_amd64.deb; sudo apt-get -yf install

RUN wget http://www.mitsuba-renderer.org/releases/current/trusty/mitsuba_0.5.0-1_amd64.deb
RUN sudo dpkg -i mitsuba_0.5.0-1_amd64.deb; sudo apt-get -yf install
