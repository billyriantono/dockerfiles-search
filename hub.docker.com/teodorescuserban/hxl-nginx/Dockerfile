FROM teodorescuserban/hdx-base-nginx:latest

MAINTAINER Serban Teodorescu, teodorescu.serban@gmail.com

#RUN mv /etc/nginx /etc/nginx.original
ADD nginx /etc/nginx

ADD run_nginx /etc/service/nginx/run
RUN chmod +x /etc/service/nginx/run && \
    rm /etc/nginx/sites-enabled/* && \
    ln -sf /etc/nginx/hxl_proxy.conf /etc/nginx/sites-enabled/proxy && \
    ln -sf /etc/nginx/hxl_beta_proxy.conf /etc/nginx/sites-enabled/beta_proxy

EXPOSE 80
EXPOSE 443

VOLUME ["/srv/www", "/var/log/nginx", "/etc/nginx", "/tmp"]

RUN /etc/my_init.d/00_regen_ssh_host_keys.sh

CMD ["/sbin/my_init"]
