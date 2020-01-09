
from nginx

RUN apt-get update -y && apt-get install -y wget
RUN apt-get -y install vim
RUN mkdir temp && cd temp/
RUN wget https://raw.githubusercontent.com/minepicco/temp/master/index.html
RUN wget https://raw.githubusercontent.com/minepicco/temp/master/default.conf
RUN wget https://raw.githubusercontent.com/minepicco/temp/master/test/ghost.jpg
RUN wget https://raw.githubusercontent.com/minepicco/temp/master/test/transparent.png
RUN wget https://raw.githubusercontent.com/minepicco/temp/master/test/worldmap.svg
RUN wget https://raw.githubusercontent.com/minepicco/temp/master/test/amesh.bmp
RUN wget https://raw.githubusercontent.com/minepicco/temp/master/test/test.css
RUN chmod +x *.*
RUN mkdir /usr/share/nginx/html/css
RUN mkdir /usr/share/nginx/html/img
RUN mv -f default.conf /etc/nginx/conf.d/
RUN mv -f index.html /usr/share/nginx/html/
RUN mv -f test.css /usr/share/nginx/html/css/
RUN mv -f *.* /usr/share/nginx/html/img/

RUN openssl req -subj "/C=JP/ST=Kanagawa/L=Yokohama/O=MNC Company/OU=MNC/CN=test.com" -newkey rsa:2048 -nodes -keyout server.key -out server.csr
RUN openssl x509 -days 3650 -req -signkey server.key < server.csr > server.crt
RUN mv server.* /etc/nginx/conf.d/
RUN chown root:root /etc/nginx/conf.d/server.*

EXPOSE 80 443
