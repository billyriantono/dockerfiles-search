FROM nginx:1.13.3

# Set up Nginx
ADD build/nginx-www.conf /etc/nginx/nginx.conf
ADD build/nginx-api-default.conf /etc/nginx/conf.d/default.conf

ENV APPDIR=/code
WORKDIR $APPDIR

# Note that static files from django are served from /code/staticfiles
