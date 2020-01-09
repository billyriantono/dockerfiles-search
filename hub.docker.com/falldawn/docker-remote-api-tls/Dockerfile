FROM nginx:1.15.10-alpine
MAINTAINER FallDawn <QiuFengXiaoShi@Gmail.Com>
RUN sed -i 's/user\s*nginx;/user root;/g' /etc/nginx/nginx.conf && \
	rm -f /etc/nginx/conf.d/*
COPY nginx.conf /etc/nginx/conf.d/nginx.conf