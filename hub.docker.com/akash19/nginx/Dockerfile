# base image
FROM nginx


COPY  fastcgi_params /etc/nginx/fastcgi_params

COPY  fastcgi.conf /etc/nginx/fastcgi.conf

COPY  koi-utf /etc/nginx/koi-utf

COPY  koi-win /etc/nginx/koi-win

COPY  mime.types /etc/nginx/ime.types

COPY  nginx.conf /etc/nginx/nginx.conf


COPY  proxy_params /etc/nginx/proxy_params

COPY  uwsgi_params /etc/nginx/uwsgi_params


COPY  scgi_params /etc/nginx/scgi_params


COPY  win-utf /etc/nginx/win-utf



RUN mkdir -p /var/www/html

COPY ./index.html /var/www/html

RUN mkdir /etc/nginx/sites-available

COPY ./sites-available/default /etc/nginx/sites-available

RUN rm /etc/nginx/conf.d/default.conf


RUN mkdir /etc/nginx/sites-enabled

RUN ln -s /etc/nginx/sites-available/default /etc/nginx/sites-enabled


# expose port 80 for network
EXPOSE 80


# start nginx service
CMD ["nginx","-g","daemon off;"]
