FROM gliderlabs/alpine
RUN sed -i 's/v3.1/edge/' /etc/apk/repositories && \
  apk update && \
  apk add syncthing
VOLUME /data
CMD ["syncthing", "-home", "/data/syncthing", "-gui-address", "0.0.0.0:8080"]
EXPOSE 8080 22000
