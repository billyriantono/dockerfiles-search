FROM alpine

RUN apk update 
RUN apk add curl
RUN apk add run-parts

COPY  ./entrypoint.sh /entrypoint.sh
RUN    \
      cp -rp /etc/crontabs /etc/crontabs.bkp && \
      chmod 755 /entrypoint.sh


ENTRYPOINT [ "/entrypoint.sh" ]

#CMD crond -f -d 6
CMD [ "crond" , "-f" , "-d" , "6" ]

VOLUME ["/etc/crontabs" , "/var/log/crontabs" , "/etc/periodic/15min" , "/etc/periodic/daily" , "/etc/periodic/hourly" , "/etc/periodic/minute" , "/etc/periodic/weekly" , "/etc/periodic/monthly" ]

