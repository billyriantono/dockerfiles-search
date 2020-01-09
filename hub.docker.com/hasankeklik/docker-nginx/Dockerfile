FROM nginx:1.15.1-alpine
RUN mkdir /etc/nginx/log/
RUN mkdir /etc/nginx/run/
COPY nginx.conf /etc/nginx/nginx.conf
COPY servers.conf /etc/nginx/servers.conf