FROM alpine

RUN mkdir /hostetc /hostopt
COPY run.sh /run.sh
COPY route.sh /route.sh
COPY crontab /crontab
VOLUME /hostetc
VOLUME /hostopt
CMD ["/run.sh"]
