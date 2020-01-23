FROM debian:stretch-slim
LABEL maintainer="asanti3@xtec.cat"

RUN apt-get -y update && \
	apt-get -y install --no-install-recommends apache2 && \ 
	apt-get clean && \
	ln -sf /dev/stdout /var/log/apache2/access.log && \
	ln -sf /dev/stderr /var/log/apache2/error.log 
	#echo "My name was once \"Happy Dijkstra\"" > /etc/apache2/conf-enabled/serverName.conf
COPY el-meu-index-cutre.html /var/www/html/index.html

EXPOSE 80
ENTRYPOINT ["apache2ctl", "-DFOREGROUND"]

