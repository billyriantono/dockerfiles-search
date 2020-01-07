FROM python:3.6
MAINTAINER Alex Deng <azkdeng@gmail.com>

RUN apt-get update -qy
RUN apt-get install -y unzip xvfb libxi6 libgconf-2-4

# Install geckodriver
RUN wget https://github.com/mozilla/geckodriver/releases/download/v0.20.1/geckodriver-v0.20.1-linux64.tar.gz
RUN tar -xvzf geckodriver*
RUN chmod +x geckodriver
RUN mv geckodriver /usr/local/bin

# Install chrome
RUN wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
RUN dpkg -i google-chrome*.deb || true
RUN apt-get -f install -y

# Install chromedriver
RUN wget https://chromedriver.storage.googleapis.com/2.39/chromedriver_linux64.zip
RUN unzip chromedriver_linux64.zip
RUN chmod +x chromedriver
RUN mv -f chromedriver /usr/local/share/chromedriver
RUN ln -s /usr/local/share/chromedriver /usr/local/bin/chromedriver
RUN ln -s /usr/local/share/chromedriver /usr/bin/chromedriver
