FROM nginx:alpine
RUN mkdir /etc/nginx/ssl
ADD public /usr/share/nginx/html/
ADD certs /etc/nginx/ssl/
ADD nginx/default.conf /etc/nginx/conf.d/
CMD ["nginx", "-g", "daemon off;"]