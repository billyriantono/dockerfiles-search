FROM nginx

COPY qa.conf /etc/nginx/conf.d/default.conf
COPY files/ /usr/share/nginx/html/

CMD [ "nginx", "-g", "daemon off;" ]
