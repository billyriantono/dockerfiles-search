FROM nginx:alpine

ADD https://raw.githubusercontent.com/Naugh/LoadTesting/master/DockerImages/Angular/nginx.conf /etc/nginx/nginx.conf

WORKDIR /usr/share/nginx/html
ADD https://raw.githubusercontent.com/Naugh/LoadTesting/master/DockerImages/Angular/LoadTestingAngular.tar.gz .
RUN tar -xzf LoadTestingAngular.tar.gz -C /usr/share/nginx/html/ \
	&& rm LoadTestingAngular.tar.gz

