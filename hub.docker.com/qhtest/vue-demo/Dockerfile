FROM nginx
RUN apt-get update && apt-get install vim -y && rm -rf /usr/share/nginx/html/index.html
COPY index.html /usr/share/nginx/html/
EXPOSE 80
