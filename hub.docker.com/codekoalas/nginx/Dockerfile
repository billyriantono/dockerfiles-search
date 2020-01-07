FROM nginx

# Install Confd
ADD https://github.com/kelseyhightower/confd/releases/download/v0.13.0/confd-0.13.0-linux-amd64 /usr/local/bin/confd
RUN chmod +x /usr/local/bin/confd

ADD nginx.conf /etc/nginx/nginx.conf
ADD confd /etc/confd

CMD ["sh", "-c", "/usr/local/bin/confd -onetime -backend env; nginx -g 'daemon off;'"]
