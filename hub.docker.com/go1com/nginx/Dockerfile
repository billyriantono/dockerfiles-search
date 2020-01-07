FROM nginx:alpine
COPY real-ip.conf /etc/nginx/conf.d/
RUN sed -i "s/ nginx;/ root;/g" /etc/nginx/nginx.conf
