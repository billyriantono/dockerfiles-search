FROM gns3/webterm
MAINTAINER Simon DECAESTECKER <contact@simondecaestecker.com>

RUN apt-get update -y && \
    apt-get install -y apache2 filezilla python

ADD entrypoint.sh /entrypoint.sh
RUN chmod +x entrypoint.sh
CMD [ "/entrypoint.sh" ]
