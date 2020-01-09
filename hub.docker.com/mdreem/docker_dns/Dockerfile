FROM ubuntu:16.04

USER root
RUN apt-get update \
	&& apt-get install -y dnsmasq supervisor python-flask python-pip \
    && pip2 install flask_restful \
    && apt-get purge python-pip -y \
    && apt-get --purge autoremove -y \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
COPY files/dnsmasq.conf /etc/dnsmasq.conf
COPY files/supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY files/update_dnsmasq.py /bin/update_dnsmasq.py
RUN chmod +x /bin/update_dnsmasq.py
CMD /usr/bin/supervisord
