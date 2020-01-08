FROM tutum/ubuntu:trusty
MAINTAINER fishcried

RUN apt-get -y update 
RUN apt-get install -y unzip 
RUN apt-get install -y python-pip
RUN apt-get install -y libmysqlclient-dev
RUN apt-get install -y python-dev

RUN pip install -v Django==1.5.10 
RUN pip install MySQL-python 
RUN pip install eventlet 
RUN pip install kombu  
RUN pip install librabbitmq  
RUN pip install prettytable  
RUN pip install argparse  
RUN pip install Pympler  
RUN pip install requests 
RUN pip install south 
RUN pip install sphinxcontrib-httpdomain

RUN wget https://github.com/rackerlabs/stacktach/archive/master.zip 
RUN unzip master.zip 
RUN rm master.zip   
RUN mkdir -p /srv/www 
RUN mv stacktach-master /srv/www/stacktach 
ADD stacktach.sh /srv/www/stacktach/run.sh
RUN chmod u+x /srv/www/stacktach/run.sh
RUN ln -s /srv/www/stacktach stacktach

EXPOSE 8000
