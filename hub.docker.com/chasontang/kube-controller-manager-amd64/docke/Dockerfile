FROM alpine:3.10.3
LABEL Author="Charles Stover"
WORKDIR /home

# Dependencies
RUN apk update
RUN apk upgrade
RUN apk add bash certbot libressl nginx

# Copy
COPY src/etc/nginx/nginx.conf /etc/nginx/nginx.conf
COPY src/home/cert.sh /home/cert
COPY src/home/crontab.txt /home/crontab.txt
COPY src/home/dhparam.sh /home/dhparam.sh
COPY src/home/entrypoint.sh /home/entrypoint.sh

# Install
RUN /usr/bin/crontab /home/crontab.txt
RUN mkdir /var/www/letsencrypt
RUN chmod +x /home/cert

# Clean Up
RUN rm -rf /home/crontab.txt

# Run
ENTRYPOINT [ "/bin/bash", "/home/entrypoint.sh" ]

EXPOSE 80 443
