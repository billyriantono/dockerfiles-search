FROM nginx:latest

MAINTAINER Ben M <git@bmagg.com>

# Add customised config files
ADD nginx.conf /etc/nginx/
ADD php.conf /etc/nginx/sites-available/

# Empower `www-data` user 
RUN usermod -u 1000 www-data

# Start up nginx
CMD ["nginx"]

# Expose ports
EXPOSE 80 443
