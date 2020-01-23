FROM ubuntu:18.04
FROM python:3.6

RUN apt-get update
RUN apt-get install -y vim
# Install x11vnc.
RUN cp /etc/apt/sources.list /etc/apt/sources.list.orig
# RUN vi /etc/apt/sources.list
RUN apt-get update && apt-get clean && apt-get install -y \
    x11vnc \
    xvfb \
    fluxbox \
    wmctrl \
    wget \
    && wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - \
    && echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list \
    && apt-get update && apt-get -y install google-chrome-stable

RUN mkdir /code
COPY . /code

WORKDIR /code

RUN pip install -r requirements.txt

# set env variables
ENV mail_trigger=False 

CMD 'runchrome.sh'