FROM ubuntu:14.04

MAINTAINER yfernando

# Install Ngnix
RUN sudo apt-get update
RUN sudo apt-get install -y nginx

# Append "daemon off;" to the beginning of the configuration
RUN echo "daemon off;" >> /etc/nginx/nginx.conf

#ADD hello.html /usr/share/nginx/html/index.html
RUN rm /usr/share/nginx/html/index.html

# Run nginx
CMD ["nginx"]
