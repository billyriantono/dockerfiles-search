FROM alpine
RUN apk update
RUN apk add transmission-daemon gettext
RUN mkdir -p /var/lib/transmission /etc/transmission
VOLUME /var/lib/transmission
EXPOSE 80
EXPOSE 51413
EXPOSE 51413/UDP
CMD ["/start.sh"]
COPY start.sh /
