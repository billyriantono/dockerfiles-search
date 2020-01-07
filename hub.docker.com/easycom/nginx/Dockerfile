FROM nginx:alpine
MAINTAINER Frédéric TURPIN <lumiru@turp.in>

## ================================
## INSTALLATION PART
## ================================

# Copy default-website for Nginx
ADD ./nginx.vh.default.conf /etc/nginx/conf.d/default.conf

# Copy nginx configuration
ADD ./nginx.conf /etc/nginx/nginx.conf

## ================================
## LAUNCH PART
## ================================
# Expose sockets
EXPOSE 80

VOLUME /srv
VOLUME /etc/nginx/conf.d
