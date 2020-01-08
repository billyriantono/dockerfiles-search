FROM danbelden/ubuntu-rabbitmq36
MAINTAINER nagnedra babu <ndonthinli@gmail.com> 

RUN apt-get update \
    && apt-get -y install wget \
    && apt-get -y install curl \
    && apt-get -y install unzip \
    && apt-get -y install apache2
    
ENV SRV_REVERSE_PROXY_DOMAIN="" \ 
    SRV_REVERSE_PROXY_CLIENT_IP_HEADER=X-Forwarded-For \ 
    SRV_SSL=0 \ 
    SRV_AUTH=0 \ 
    SRV_ADMIN="" \ 
    SRV_NAME="" \ 
    SRV_DOCROOT="" \ 
    SRV_PHP=0 \ 
    SRV_PHP_HOST=php \ 
    SRV_PHP_PORT=9000 \ 
    SRV_LETSENCRYPT=false \ 
    SRV_CERT="" \ 
    SRV_CERT_KEY="" 

COPY docker-healthcheck /usr/local/bin/

HEALTHCHECK --interval=5s --timeout=3s CMD curl --fail http://localhost:5672/pools || exit 1

#HEALTHCHECK CMD ["docker-healthcheck"]
#COPY apache2 /usr/local/apache2 
#RUN chmod +x /usr/local/apache2/bin/start.sh 
EXPOSE 80 5671 5672 15671 15672 
#CMD ["/usr/local/apache2/bin/start.sh"]