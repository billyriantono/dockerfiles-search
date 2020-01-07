FROM nginx
MAINTAINER Kevin Wiesmüller

RUN sed -i 'N; s/root   \/usr\/share\/nginx\/html;\n        index  index.html index.htm;/root   \/usr\/share\/nginx\/html;\n        autoindex on;/' /etc/nginx/conf.d/default.conf
RUN sed --in-place 's/listen\s*80;/listen       8080;/' /etc/nginx/conf.d/default.conf