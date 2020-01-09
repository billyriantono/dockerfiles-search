FROM gliderlabs/registrator

COPY ./init-registrator.sh /init-registrator.sh
RUN chmod +x /init-registrator.sh

ENTRYPOINT ["/init-registrator.sh"]
CMD ["consul://localhost:8500"]