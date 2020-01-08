FROM dvdgiessen/nginx-rtmp-docker
COPY ./default /usr/local/nginx/conf/default
COPY ./nginx.conf /usr/local/nginx/conf/nginx.conf
COPY ./initializate.sh /initializate.sh
CMD /initializate.sh && /usr/local/nginx/sbin/nginx -c /usr/local/nginx/conf/nginx.conf
