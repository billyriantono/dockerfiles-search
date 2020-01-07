FROM jakubigla/nginx

MAINTAINER Jakub Igla <jakub.igla@gmail.com>

RUN rm -rf /etc/nginx/sites-available/default
ADD ./conf/sites-available/default /etc/nginx/sites-available/

CMD ["nginx", "-g", "daemon off;"]