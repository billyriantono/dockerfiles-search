FROM nginx:alpine
LABEL maintainer="alexandro@autistici.org"
LABEL version="0.1"
LABEL description="This is a little webpage"
COPY nginx.conf /etc/nginx
COPY default.conf /etc/nginx/conf.d/
VOLUME /usr/share/nginx/html
EXPOSE 80
