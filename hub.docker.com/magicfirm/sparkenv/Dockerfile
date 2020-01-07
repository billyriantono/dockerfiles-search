# ------------------------------------------------------------------------------
# This image used in magicfirm spark cloud running enviroment.
# ------------------------------------------------------------------------------
# Pull base image.
FROM ubuntu:16.04
MAINTAINER JIN TAO <jeffkyjin@magicfirm.com>

# Install relates.
RUN \
        apt-get update && \
        apt-get -y install python-pip wget ruby tzdata gunicorn
  
# - update pip
RUN pip install --upgrade pip

# - Install web server
RUN pip install web.py uwsgi simplejson requests
        
# - Install numpy
RUN pip install numpy numpy-stl
        
# - Install mersh
RUN gem install mersh

# setting timezone
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
