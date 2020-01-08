FROM ubuntu:14.04

# REPOS
RUN apt-get update; apt-get install -y -q software-properties-common python-software-properties

# DEFAULT
RUN apt-get install -y -q curl git make wget openssh-server zip tmux vim nano python python-setuptools nginx sudo

# SUPERVISOR
RUN easy_install supervisor
