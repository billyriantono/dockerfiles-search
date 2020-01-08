FROM nginx

ADD run.sh /opt/
RUN chmod +x /opt/run.sh

ENV PORT 80

WORKDIR /opt
CMD ["/opt/run.sh"]
