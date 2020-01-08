FROM nginx:latest
ENV CLIENT_SECURITY aes-128-gcm
ENV UUID 0
ENV DOMAIN_NAME 0

ADD app/v2ray /usr/local/bin/
ADD app/caddy /usr/local/bin/
ADD app/v2ctl /usr/local/bin/

ADD entrypoint.sh /etc

RUN chmod +x /etc/entrypoint.sh 
RUN chmod 777 /usr/local/bin/v2ray 
RUN chmod 777 /usr/local/bin/caddy 
RUN chmod 777 /usr/local/bin/v2ctl 
RUN chmod 777 /etc/entrypoint.sh 
RUN mkdir /var/log/v2ray 
RUN mkdir /var/log/caddy 
RUN mkdir /etc/v2ray 
RUN mkdir /etc/caddy 
RUN chmod -R 777 /etc/v2ray 
RUN chmod -R 777 /etc/caddy 
RUN chmod -R 777 /var/log/

ADD conf/caddy.conf /etc/caddy/caddy.conf
ADD conf/v2ray.json /etc/v2ray/v2ray.json

ENTRYPOINT  /etc/entrypoint.sh

EXPOSE 8080
