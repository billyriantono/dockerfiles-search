FROM nginx
COPY conf /etc/nginx/

COPY conf/sites-available /etc/nginx/sites-enabled
COPY crossdomain.xml /usr/share/nginx/html

EXPOSE 80 443 8000 8001

ENTRYPOINT ["nginx", "-g", "daemon off;"]