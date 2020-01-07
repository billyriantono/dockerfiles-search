FROM tutum/influxdb:0.9

ADD config.toml /config/config.toml

ENV PRE_CREATE_DB **None**
ENV SSL_SUPPORT **False**
ENV SSL_CERT **None**

# Admin server WebUI
EXPOSE 8083

# HTTP API
EXPOSE 8086

VOLUME ["/data"]

CMD ["/run.sh"]
