# nginx Dockerfile
FROM nginx:latest
RUN rm /etc/nginx/conf.d/default.conf
COPY frontend-build /usr/share/nginx/html
ADD frontend-server.conf /etc/nginx/conf.d/frontend-server.conf
ADD django-server.conf /etc/nginx/conf.d/django-server.conf
ADD nginx.conf /etc/nginx/nginx.conf