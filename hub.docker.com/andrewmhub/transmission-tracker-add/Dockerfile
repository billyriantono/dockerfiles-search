FROM alpine:latest

ENV TORRENTLIST=https://raw.githubusercontent.com/ngosang/trackerslist/master/trackers_all.txt

COPY ./tracker-add-auto.sh /opt/tracker-add-auto.sh

RUN apk add --update \
        bash transmission-cli curl coreutils && \
        rm -rf /var/cache/apk/* && \
        chmod +x /opt/tracker-add-auto.sh

USER guest
ENTRYPOINT [ "/opt/tracker-add-auto.sh" ]