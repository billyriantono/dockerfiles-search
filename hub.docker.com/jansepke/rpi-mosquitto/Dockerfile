FROM arm32v6/alpine:3.7
COPY tmp/qemu-arm-static /usr/bin/qemu-arm-static

ARG BUILD_DATE
ARG VCS_REF

LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.vcs-url="https://github.com/jansepke/rpi-mosquitto.git" \
      org.label-schema.vcs-ref=$VCS_REF

RUN apk --no-cache add mosquitto
COPY mosquitto.conf /etc/mosquitto/
VOLUME ["/var/lib/mosquitto"]

EXPOSE 1883 9001
CMD ["/usr/sbin/mosquitto", "-c", "/etc/mosquitto/mosquitto.conf"]