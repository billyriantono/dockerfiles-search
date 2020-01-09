FROM ubuntu:xenial
MAINTAINER Dennis Schaaf <dennis@plantdemand.com>

# Update packages

RUN sed 's/main$/main universe/' -i /etc/apt/sources.list
RUN apt-get update -qq
RUN apt-get upgrade -y -qq

# Set Locale

RUN apt-get install -y locales locales-all
ENV LC_ALL en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US.UTF-8
ENV DEBIAN_FRONTEND noninteractive

# Download and install wkhtmltopdf
RUN apt-get install -y -qq build-essential xorg libssl-dev libxrender-dev wget --quiet gdebi
# RUN wget --quiet http://download.gna.org/wkhtmltopdf/0.12/0.12.2.1/wkhtmltox-0.12.2.1_linux-trusty-amd64.deb
# RUN gdebi --n wkhtmltox-0.12.2.1_linux-trusty-amd64.deb
RUN apt-get install -y -qq wkhtmltopdf

# Install other important tools

RUN apt-get install -y  -qq git libmysqlclient-dev  wget libxml2-dev libxslt-dev curl

# Python Environment

RUN apt-get install -y  -qq python3-pip python3-dev python-virtualenv 
RUN apt-get install -y  -qq awscli jq


# Install Node 4.x
# RUN curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -

RUN apt-get install -y  -qq nodejs 
RUN ln -sf  /usr/bin/nodejs /usr/bin/node

# Prepare environment

COPY docker_entry_point.sh /docker_entry_point.sh
COPY virtual_env_entry_point.sh /virtual_env_entry_point.sh
COPY virtual_env_setup.sh /virtual_env_setup.sh
RUN chmod 755 /*.sh

COPY requirements.txt requirements.txt
COPY package.json package.json
RUN /virtual_env_setup.sh


RUN mkdir /root/.ssh
COPY known_hosts /root/.ssh/known_hosts
COPY user_ssh_config /root/.ssh/config
RUN chmod 600 ~/.ssh/known_hosts
RUN chmod 700 ~/.ssh



CMD ["/bin/sh", "/docker_entry_point.sh"]
