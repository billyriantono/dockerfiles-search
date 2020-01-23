FROM  ubuntu

RUN apt-get update && apt-get install -y nano && apt-get install -y nginx

EXPOSE 80

COPY web/index.html /var/www/html/

CMD  ["nginx","-g","daemon off;"]
