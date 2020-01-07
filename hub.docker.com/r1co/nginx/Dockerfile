FROM nginx

RUN apt-get update && apt-get install -y supervisor python3

RUN mkdir -p /var/log/supervisor

ADD supervisord/supervisord.conf /etc/supervisor/conf.d/supervisord.conf
ADD supervisord/nginx.conf /etc/supervisor/conf.d/nginx.conf

# Add copy volume script 
RUN mkdir -p /app
ADD copy-volume.sh /app
RUN chmod +x /app/copy-volume.sh

RUN mkdir -p /app/template/etc/
RUN cp -r /etc/nginx/ /app/template/etc

ENV CONFIG_TEMPLATES="/app/template/etc/nginx:/etc/nginx/"


CMD /app/copy-volume.sh && /usr/bin/supervisord


