FROM ubuntu:18.04
RUN apt-get clean
RUN apt-get update
RUN apt-get install -y sudo cron nginx
RUN apt-get install -y nano net-tools 
RUN apt-get install -y gradle curl rsyslog
RUN mkdir script
COPY script-autoarranque.sh /script/script-autoarranque.sh
COPY script-reinicioServer.sh /script/script-reinicioServer.sh
RUN chmod -R 777 /script/*
ADD crontab /etc/cron.d/root
COPY crontab /var/spool/cron/crontabs/root
RUN echo exit 0 > /usr/sbin/policy-rc-d
#RUN (crontab -l && echo "*/1 * * * * sudo -u root /script/script-reinicioServer.sh") | crontab -
CMD ["/script/script-autoarranque.sh ;; /bin/bash"]
