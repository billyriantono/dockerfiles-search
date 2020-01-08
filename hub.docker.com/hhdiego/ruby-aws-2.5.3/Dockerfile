FROM ruby:2.6.3

# APT-GET UTILS
RUN apt-get update && apt-get install -y --no-install-recommends apt-utils

# INSTALL PYTHON-DEV AND PIP
RUN apt-get update && apt-get install -y python2.7 python-pip gcc imagemagick

# INSTALL AWS-CLI
RUN pip install awsebcli --upgrade
RUN pip install awscli --upgrade

