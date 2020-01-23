FROM centos:centos6

MAINTAINER gupta.atmakuri@gmail.com 

# Enable EPEL for Node.js
RUN rpm -Uvh http://download.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm

# Install Node...
RUN yum install -y nginx

# Install Node...
RUN yum install -y npm

# Install app and dependencies into /src
RUN mkdir /var/www/html && cd /var/www/html; npm install

# Copy app to html 
COPY . /var/www/html
COPY nginx.conf /etc/nginx
RUN service nginx restart

EXPOSE 80
