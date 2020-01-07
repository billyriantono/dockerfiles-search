FROM  debian:8

LABEL service=nginx

WORKDIR /app

RUN apt-get update && \
    apt-get install -y wget && \
    wget http://nginx.org/keys/nginx_signing.key && \
    apt-key add nginx_signing.key && \
    rm -fr nginx_signing.key && \
    {  \
     echo deb http://nginx.org/packages/debian/ jessie nginx; \
     echo deb-src http://nginx.org/packages/debian/ jessie nginx; \
    }  >  /etc/apt/sources.list.d/nginx.list  &&  \
    apt-get update  && \
    apt-get install -y nginx && \
    apt-get purge -y wget && \
    apt-get autoremove -y && \
    apt-get clean && \
    rm -fr  /var/lib/apt/lists && \
    rm -rf /etc/nginx/conf.d && \
    mkdir /conf && \
    ln -s /conf /etc/nginx/conf.d 

ADD nginx.conf /etc/nginx/nginx.conf
ADD conf.d/* /conf/

EXPOSE 80 443

CMD ["nginx"]
