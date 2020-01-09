FROM debian:wheezy

RUN apt-get update && apt-get install -y nginx \
    && rm -rf /var/lib/apt/lists/*

RUN echo "<!DOCTYPE html><html><head><meta charset=utf-8></head><body>Hi ٩( 'ω' )و</body></html>" > /usr/share/nginx/www/index.html

CMD ["nginx", "-g", "daemon off;"]

EXPOSE 80
