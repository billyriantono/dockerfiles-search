FROM nginx:alpine

RUN ln -snf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo "Asia/Shanghai" > /etc/timezone
	
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf

WORKDIR /var/www/html/
