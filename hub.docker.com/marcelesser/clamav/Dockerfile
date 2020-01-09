FROM alpine:latest
RUN apk --no-cache --update upgrade
RUN apk --no-cache --update add clamav-daemon \
  clamav-scanner \
  clamav-libunrar
RUN freshclam
ADD ./clamd.conf /etc/clamav/clamd.conf
ADD ./freshclam.conf /etc/clamav/freshclam.conf
ADD ./entrypoint.sh /entrypoint.sh

RUN freshclam

EXPOSE 3310

CMD ["/entrypoint.sh"]
