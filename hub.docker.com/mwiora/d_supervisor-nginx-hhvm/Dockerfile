from mwiora/d_supervisor-nginx
MAINTAINER Matthias R. Wiora "matthias@wiora.co.uk"

# installation instructions reg. https://docs.hhvm.com/hhvm/installation/linux#ubuntu-14.04-trusty
RUN apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0x5a16e7281be7a449 \
	&& echo "deb http://dl.hhvm.com/ubuntu $(lsb_release -sc) main" >> /etc/apt/sources.list \
	&& apt-get update \
	&& apt-get install hhvm -y \
	&& rm -rf /var/lib/apt/lists/*

RUN mkdir -p /var/www

COPY default /etc/nginx/sites-available/default

COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
EXPOSE 80 443

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]
