# ----- Dockerfile to build mypost-ng-cli-headless on top of mypost-ng-cli base container
# docker build {--build-arg NG_CLI_VERSION=1.6.6} -t mypost-ng-cli .

FROM benboarder/mypost-ng-cli:latest

LABEL name="mypost-ng-cli-karma" \
      maintainer="DDCTeamWookie <DLDDCTeamWookie@auspost.com.au>" \
      version="1.0" \
      description="The headless docker container for MyPost Consumer automated testing"

ENV TZ="/usr/share/zoneinfo/Australia/Melbourne"
ENV LANG C.UTF-8
ENV NPM_CONFIG_LOGLEVEL warn

USER root

ADD display-chromium /usr/bin/display-chromium
ADD xvfb-chromium /usr/bin/xvfb-chromium
ADD xvfb-chromium-webgl /usr/bin/xvfb-chromium-webgl

RUN apt-get update \
    && apt-get install -y \
      xvfb \
      libosmesa6 \
      libgconf-2-4 \
 && wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb \
 && (dpkg -i google-chrome-stable_current_amd64.deb; apt-get -fy install; rm google-chrome-stable_current_amd64.deb; apt-get clean; rm -rf /var/lib/apt/lists/* ) \
 && mv /usr/bin/google-chrome /usr/bin/google-chrome.real  \
 && mv /opt/google/chrome/google-chrome /opt/google/chrome/google-chrome.real  \
 && rm /etc/alternatives/google-chrome \
 && ln -s /opt/google/chrome/google-chrome.real /etc/alternatives/google-chrome \
 && ln -s /usr/bin/xvfb-chromium /usr/bin/google-chrome \
 && ln -s /usr/bin/xvfb-chromium /usr/bin/chromium-browser \
 && ln -s /usr/lib/x86_64-linux-gnu/libOSMesa.so.6 /opt/google/chrome/libosmesa.so

USER $USER_ID
