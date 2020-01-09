FROM eclipse-mosquitto:1.6.8@sha256:d7a333b55c1b97d1ff6098a9f9771c9adc8f8b24c4136ccd5bf88ab80e50675b

COPY docker-entrypoint.sh /

ENTRYPOINT ["sh", "./docker-entrypoint.sh"]

CMD ["/usr/sbin/mosquitto", "-c", "/mosquitto/config/mosquitto.conf"]
