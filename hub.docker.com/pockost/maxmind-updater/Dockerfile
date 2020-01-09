FROM alpine:latest

ENV DB_DEST /database
ENV TMP_FOLDER /tmp
ENV PRODUCT_IDS GeoLite2-City GeoLite2-Country GeoLite2-ASN
ENV CRONTAB_FREQUENCY 0 0 * * 1

RUN apk add --no-cache curl tar

COPY entrypoint.sh /entrypoint.sh
COPY update-maxmind.sh /update-maxmind.sh

RUN chmod +x /entrypoint.sh /update-maxmind.sh

ENTRYPOINT ["/entrypoint.sh"]
CMD ["crond", "-l2", "-f"]
