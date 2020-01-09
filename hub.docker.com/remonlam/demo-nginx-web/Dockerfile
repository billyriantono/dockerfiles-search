FROM remonlam/demo-alpine-nginx:1.15.3

LABEL maintainer="Remon Lam <remon.lam@rechtspraak.nl>"

COPY index.html /usr/share/nginx/html/
COPY 50x.html /usr/share/nginx/html/
COPY css/normalize.css /usr/share/nginx/html/css/
COPY css/skeleton.css /usr/share/nginx/html/css/
COPY images/*.gif /usr/share/nginx/html/
COPY node.txt /usr/share/nginx/html/
CMD hostname > /usr/share/nginx/html/node.txt ; nginx -g "daemon off;"
