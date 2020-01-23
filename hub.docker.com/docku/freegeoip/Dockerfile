FROM dock0/service
MAINTAINER Jon Chen <bsd@voltaire.sh>

EXPOSE 80

ENV FREEGEOIP_HOST_PORT "0.0.0.0:80"
ENV FREEGEOIP_VERSION "3.0.4"
ENV FREEGEOIP_PATH "/usr/sbin/freegeoip"

ADD https://dl.bintray.com/jchen/docku/$FREEGEOIP_VERSION/freegeoip $FREEGEOIP_PATH
RUN chmod +x $FREEGEOIP_PATH

ADD run /service/freegeoip/run
