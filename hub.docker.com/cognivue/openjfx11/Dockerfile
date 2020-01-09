FROM ubuntu:18.04
RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y openjdk-11-jdk-headless openjfx git sudo lshw xvfb
RUN export DISPLAY=:99.0
RUN xvfb :99 -ac & 