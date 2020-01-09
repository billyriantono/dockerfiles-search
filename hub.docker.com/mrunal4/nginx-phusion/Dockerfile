FROM phusion/baseimage

# Use baseimage-docker's init system.
CMD ["/sbin/my_init"]

# install nginx
RUN apt update    &&    apt install -y nginx

# create directory nginx in /etc/service/
RUN mkdir /etc/service/nginx

# copy all content from pwd (from where build is triggered) in /etc/service/nginx/
ADD ./nginx /etc/service/nginx/

# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
