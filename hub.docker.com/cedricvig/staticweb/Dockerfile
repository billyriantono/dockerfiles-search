FROM ubuntu:14.04
RUN apt-get update
RUN apt-get install -y nginx
RUN echo '<!DOCTYPE html> <html><head></head><body>Salut tous! - Static website...</body></html>' \
    >/usr/share/nginx/html/index.html
CMD [ "nginx", "-g", "daemon off;" ]
EXPOSE 80
