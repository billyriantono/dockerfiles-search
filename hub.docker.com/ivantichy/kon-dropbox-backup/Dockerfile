FROM mhimmer/dropbox

COPY *.sh /

VOLUME /var/docker-data/

RUN echo "0 2 * * * root /backupjira.sh >> /var/log/backupjira.log 2>&1" > /etc/cron.d/backupcron && echo >> /etc/cron.d/backupcron

ENTRYPOINT [ "/entrypoint.sh" ]



 
 
