FROM nginx:latest
LABEL maintainer="thiswind@gmail.com"
RUN rm -rf /usr/share/nginx/html
ADD html /usr/share/nginx/html
RUN chmod -R 755 /usr/share/nginx/html
