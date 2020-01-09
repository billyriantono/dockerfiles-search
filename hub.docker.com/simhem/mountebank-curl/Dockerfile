FROM andyrbell/mountebank

RUN apk --no-cache add curl

COPY entry_point.sh /opt/bin/entry_point.sh

#RUN dos2unix /opt/bin/entry_point.sh
RUN chmod +x /opt/bin/entry_point.sh

ENTRYPOINT ["/opt/bin/entry_point.sh"]
