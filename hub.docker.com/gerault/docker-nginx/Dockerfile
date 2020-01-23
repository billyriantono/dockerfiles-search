# from debian stretch backports
FROM gerault/docker-debian-stretch-backports
MAINTAINER Mathieu Gerault <mathieu.gerault@gamil.com>
LABEL Description="Nginx server from Mathieu GERAULT"

# install nginx
RUN apt-get update \
	&& apt-get install -y nginx \
	&& apt-get clean \
	&& rm -rf /var/lib/apt/lists/*

# forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log  \
	&& ln -sf /dev/stderr /var/log/nginx/error.log 

# suppress default site
RUN rm -rf /etc/nginx/sites-enabled/default

EXPOSE 80
STOPSIGNAL SIGTERM

# nginx command
CMD ["nginx", "-g", "daemon off;"]

