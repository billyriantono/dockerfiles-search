# This is a docker build for Nginx Containers/Reverse Proxy
#

FROM byunique/trusty-base 
MAINTAINER byunique <me@brandonyu.com>

RUN apt-get update -y
RUN apt-get install nginx -y
RUN apt-get install curl -y
RUN apt-get install telnet -y


# Remove the default Nginx configuration file
# RUN rm -v /etc/nginx/nginx.conf

# Copy a configuration file from the current directory
RUN rm -v /etc/nginx/sites-enabled/*
ADD rev_proxy.conf /etc/nginx/sites-enabled

# Copy a configuration file from the current directory
# ADD nginx.conf /etc/nginx/

# Append "daemon off;" to the beginning of the configuration
# RUN echo "daemon off;" >> /etc/nginx/nginx.conf

# Expose ports
EXPOSE 80

# Set the default command to execute
# when creating a new container
CMD service nginx start

