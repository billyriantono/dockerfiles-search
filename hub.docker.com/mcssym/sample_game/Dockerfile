FROM ubuntu
LABEL maintainer="Maxime Florent F. (maxusr@gmail.com)"
LABEL version="0.0.1"
LABEL description="Try to guess the next position if the tile."
RUN apt-get update
RUN apt-get install -y nginx
COPY . /usr/share/nginx/html/
ENTRYPOINT [ "/usr/sbin/nginx", "-g", "'daemon off;'" ]
EXPOSE 80
VOLUME ["/usr/share/nginx/html"]