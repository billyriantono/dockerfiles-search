FROM prom/node-exporter

COPY alertmanager/* /etc/alertmanager/

EXPOSE 9100

CMD [ '-config.file=/etc/alertmanager/config.yml', '-storage.path=/alertmanager']