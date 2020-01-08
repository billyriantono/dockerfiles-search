FROM phusion/baseimage:0.9.10

ENV HOME /root

RUN /etc/my_init.d/00_regen_ssh_host_keys.sh
RUN /usr/sbin/enable_insecure_key

CMD ["/sbin/my_init"]

RUN apt-get update
RUN apt-get install -y mongodb
RUN sed -i.bak s/"bind_ip = 127.0.0.1"/"bind_ip = 0.0.0.0"/g /etc/mongodb.conf

#RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*



