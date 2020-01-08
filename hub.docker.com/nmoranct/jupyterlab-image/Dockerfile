# Start with python slim base
FROM python:3.6.4-slim

COPY ./ /

# Install python package and dependencies
RUN pip install -r requirement.txt

# setup crontab
RUN apt-get update
RUN apt-get -y install cron
RUN apt-get -y install curl
# required to get good performance from theano (used by pymc3)
RUN apt-get -y install python-dev g++
# some utilities to make life easier
RUN apt-get -y install vim htop less tmux

ENTRYPOINT bash start.sh
