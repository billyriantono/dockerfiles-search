FROM ubuntu:16.04
MAINTAINER ajaykangare

# install dependencies
RUN apt-get update \
	&& apt-get install -y --no-install-recommends \
		apache2 \
	&& rm -r /var/lib/apt/lists/*

RUN echo "#######################Github----->Dockerimage" >/var/www/html/index.html
# Default command	
CMD ["apachectl", "-D", "FOREGROUND"]
#CMD /etc/init.d/apache2 start
# Ports
EXPOSE 80
