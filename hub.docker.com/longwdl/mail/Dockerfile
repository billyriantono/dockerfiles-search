FROM ubuntu:16.04

RUN echo 'deb http://us.archive.ubuntu.com/ubuntu xenial main multiverse'|tee -a /etc/apt/sources.list

RUN apt-get update -qq && apt-get install -y sudo
RUN useradd -m mymail
RUN echo 'mymail ALL=NOPASSWD: ALL' > /etc/sudoers.d/mymail

# Run updates and prepare dependency
RUN apt-get install -y build-essential libpq-dev \
	procmail ssmtp getmail4 curl ripmime unrar \
	libreoffice cron sendemail vim

RUN apt-get clean

USER mymail
