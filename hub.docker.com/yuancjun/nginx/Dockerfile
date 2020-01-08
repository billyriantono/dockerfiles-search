FROM alpine:latest
RUN apk add openssl nginx
RUN mkdir /run/nginx
RUN rm /etc/nginx/conf.d/default.conf
RUN rm /etc/nginx/nginx.conf
ADD https://raw.githubusercontent.com/yuancjun/dockerfile/master/nginx/default.conf /etc/nginx/conf.d/default.conf
ADD https://raw.githubusercontent.com/yuancjun/dockerfile/master/nginx/dh4096.pem /etc/nginx/ssl/dh4096.pem
ADD https://raw.githubusercontent.com/yuancjun/dockerfile/master/nginx/nginx.cer /etc/nginx/ssl/nginx.cer
ADD https://raw.githubusercontent.com/yuancjun/dockerfile/master/nginx/nginx.key /etc/nginx/ssl/nginx.key
ADD https://raw.githubusercontent.com/yuancjun/dockerfile/master/nginx/nginx.conf /etc/nginx/nginx.conf
ADD https://raw.githubusercontent.com/yuancjun/dockerfile/master/nginx/run.sh /etc/nginx/run.sh
WORKDIR /app
CMD ["/bin/sh", "/etc/nginx/run.sh"]
