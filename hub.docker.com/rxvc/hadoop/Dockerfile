FROM rxvc/hadoop:2.7.7-base
MAINTAINER Rodrigo Vallejo <rxvallejoc@gmail.com>

HEALTHCHECK CMD curl -f http://localhost:8088/ || exit 1

ADD run.sh /run.sh
RUN chmod a+x /run.sh

EXPOSE 8088

CMD ["/run.sh"]
