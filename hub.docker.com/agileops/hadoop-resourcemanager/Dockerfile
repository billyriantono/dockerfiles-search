FROM agileops/hadoop-base:2.9.1-0.9
MAINTAINER michael@faille.io <michael@faille.io>

HEALTHCHECK CMD curl -f http://localhost:8088/ || exit 1

ADD run.sh /run.sh
RUN chmod a+x /run.sh

EXPOSE 8088

CMD ["/run.sh"]
