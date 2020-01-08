FROM maven:3.5.4-jdk-9

RUN apt-get update && apt-get install -y firefox

RUN wget https://github.com/mozilla/geckodriver/releases/download/v0.21.0/geckodriver-v0.21.0-linux64.tar.gz -O geckodriver.tar.gz
RUN tar xzvf geckodriver.tar.gz
RUN rm geckodriver.tar.gz

RUN mv geckodriver /usr/bin/geckodriver
