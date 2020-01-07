FROM mondayfactory/nginx-php71:latest
MAINTAINER Petr Besir Horacek <petr@mondayfactory.cz>

RUN curl --silent --location https://rpm.nodesource.com/setup_6.x | bash - && \
	yum install -y nodejs \
	gcc \
	gcc-c++ \
	git && \
	npm upgrade minimatch && npm upgrade graceful-fs && npm install -g gulp

#Set port
EXPOSE 80 443

#Start it
ENTRYPOINT ["/start.sh"]
