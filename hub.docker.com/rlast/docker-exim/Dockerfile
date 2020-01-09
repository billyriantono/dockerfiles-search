FROM alpine
RUN apk --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing add exim
RUN mkdir /var/log/exim && chown exim:exim /var/log/exim -R
COPY ./entrypoint.sh /
EXPOSE 25
USER exim
ENTRYPOINT ["/entrypoint.sh"]
CMD ["-bdf", "-q15m"]
