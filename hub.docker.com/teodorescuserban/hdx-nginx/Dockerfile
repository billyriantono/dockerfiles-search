FROM teodorescuserban/hdx-base-nginx:1.8

MAINTAINER Serban Teodorescu, teodorescu.serban@gmail.com

COPY run_nginx helper_nginx.py swup.py /srv/
COPY nginx /srv/nginx

RUN rm -rf /etc/nginx && \
    mv /srv/run_nginx /etc/service/nginx/run && \
    mv /srv/nginx /etc/ && \
    mv /srv/helper_nginx.py /srv/helper.py && \
    chmod +x /etc/service/nginx/run && \
    chmod +x /srv/swup.py && \
    ln -sf /srv/swup.py /usr/sbin/swup && \
    apt-get -qq update && apt-get -qq -y install libc-bin && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 80 443

VOLUME ["/srv/www", "/var/log/nginx", "/etc/nginx", "/tmp"]

RUN /etc/my_init.d/00_regen_ssh_host_keys.sh

CMD ["/sbin/my_init"]
