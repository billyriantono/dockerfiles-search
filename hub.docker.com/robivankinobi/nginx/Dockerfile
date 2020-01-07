# Pull base image.
FROM nginx:mainline-alpine

# File Author.
MAINTAINER Robert Hänsel <mail@hc.zone>

# add some configs
COPY *.conf /etc/nginx/
COPY sites-enabled/* /etc/nginx/sites-enabled/
COPY directive-only /etc/nginx/directive-only
COPY location /etc/nginx/location
