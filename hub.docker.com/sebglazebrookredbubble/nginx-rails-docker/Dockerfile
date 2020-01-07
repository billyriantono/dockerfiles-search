FROM nginx
ADD etc/nginx/conf.d/default.conf /etc/nginx/conf.d/default.conf
ADD etc/nginx/sites-available/ /etc/nginx/sites-available/
ADD etc/nginx/nginx.conf /etc/nginx/nginx.conf
ADD usr/local/bin/start-nginx /usr/local/bin/start-nginx
WORKDIR /etc/nginx
CMD /usr/local/bin/start-nginx
