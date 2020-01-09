FROM ubuntu:19.04
# https://askubuntu.com/questions/909277/avoiding-user-interaction-with-tzdata-when-installing-certbot-in-a-docker-contai
ENV DEBIAN_FRONTEND=noninteractive
# https://docs.google.com/spreadsheets/d/16ycob0pe97H0Bz70WWXgx1-wNp6cVr1OcdQFaf5N7s8/edit#gid=0
RUN apt update
RUN apt install -y build-essential \
                   cmake \
                   qtbase5-dev \
                   qttools5-dev \
                   qtdeclarative5-dev \
                   libqt5x11extras5-dev \
                   libqt5websockets5-dev \
                   qttools5-dev-tools


