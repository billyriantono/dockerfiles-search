FROM busybox
MAINTAINER Alban Bruder <mail@albanbruder.de>

ADD index.html /www/index.html
Add assets /www/assets

EXPOSE 8000

# Create a basic webserver and run it until the container is stopped 
CMD trap "exit 0;" TERM INT; httpd -p 8000 -h /www -f & wait
