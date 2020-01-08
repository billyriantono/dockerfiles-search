FROM ubuntu:14.04

MAINTAINER Kristof Coomans "kristof@2dotstwice.be"
ENV REFRESHED_AT "2017-02-04 11:13:00"

RUN DEBIAN_FRONTEND=noninteractive apt-get -y update
RUN DEBIAN_FRONTEND=noninteractive apt-get -y --fix-missing -q install software-properties-common
RUN LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php
RUN DEBIAN_FRONTEND=noninteractive apt-get -y update
RUN DEBIAN_FRONTEND=noninteractive apt-get -y --fix-missing -q install php5.6-cli php5.6-gd php5.6-sqlite php5.6-mysqlnd php5.6-curl php5.6-intl php5.6-xml php5.6-mbstring php5.6-json php5.6-mcrypt php5.6-bcmath php5.6-soap php5.6-zip

CMD /bin/bash
