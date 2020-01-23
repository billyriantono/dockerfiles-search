FROM ruby:latest

ENV DISPLAY :39 # there is no special reason

SHELL ["/bin/bash", "-c"]
RUN apt-get update && apt-get -y upgrade && apt-get install -y gdebi-core && \
    wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb && \
    gdebi --n google-chrome-stable_current_amd64.deb && \
    rm ./google-chrome-stable_current_amd64.deb && apt-get purge -y gdebi-core && apt-get autoremove -y && \
\
    ver_info=$(curl -fsSL https://chromedriver.storage.googleapis.com/LATEST_RELEASE) && \
    curl -fsSLo- https://chromedriver.storage.googleapis.com/${ver_info}/chromedriver_linux64.zip | funzip > /usr/local/bin/chromedriver && \
\
    apt-get install -y xvfb
