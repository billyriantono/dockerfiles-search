FROM mkenney/npm:node-8-debian

RUN apt-get update
RUN apt-get install -y nginx
Run apt-get install -y unzip
RUN npm i -g npm #Updates the npm

#Copies the nginx default configuration
RUN mv /etc/nginx/sites-available/default /etc/nginx/sites-available/def_old
COPY nginx_default_config /etc/nginx/sites-available/default
RUN nginx -t

COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

CMD ["/entrypoint.sh"]