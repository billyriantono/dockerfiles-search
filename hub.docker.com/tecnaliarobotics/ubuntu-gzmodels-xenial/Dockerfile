FROM ubuntu:xenial

RUN apt-get update && apt-get install -y -qq unzip && apt-get clean && rm -rf /var/lib/apt/lists/*

ADD https://bitbucket.org/osrf/gazebo_models/get/9533d5559309.zip /tmp/

RUN mkdir ~/.gazebo && unzip /tmp/9533d5559309.zip -d ~/.gazebo && mv ~/.gazebo/osrf-gazebo_models-9533d5559309 ~/.gazebo/models && rm /tmp/9533d5559309.zip
