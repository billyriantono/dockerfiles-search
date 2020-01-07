# Set base image as nginx 1.15
FROM nginx:1.15

# OPTIONAL: Auther of docker file
LABEL "Auther"="https://github.com/sanjay-namdeo/"

# Copy nginx conf file to ngnix root directory
COPY default.conf /etc/nginx/conf.d/

# Copy sample app into ngnix directory. This path is configured default.conf
COPY sample-app/ /usr/share/nginx/html