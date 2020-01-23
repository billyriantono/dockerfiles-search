FROM alpine
MAINTAINER Michael(Zichun) Lin <michaellin@ualberta.ca>

# basic flask environment
RUN apk add --no-cache bash git nginx uwsgi uwsgi-python3 \
	&& pip3 install --upgrade pip \
	&& pip3 install flask flask-mongoengine requests setuptools mongoengine flask-cors

# application folder
ENV APP_DIR /home/app

# app dir
RUN mkdir $APP_DIR \
	&& chown -R nginx:nginx $APP_DIR \
	&& chmod 777 /run/ -R \
	&& chmod 777 /root/ -R
VOLUME /home/app
WORKDIR $APP_DIR

# expose web server port
# only http, for ssl use reverse proxy
EXPOSE 80

# copy config files into filesystem
COPY nginx.conf /etc/nginx/nginx.conf
COPY app.ini /app.ini
COPY entrypoint.sh /entrypoint.sh

# exectute start up script
ENTRYPOINT ["/entrypoint.sh"]
