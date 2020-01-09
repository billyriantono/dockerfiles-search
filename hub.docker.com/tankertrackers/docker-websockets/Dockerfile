FROM breki/common

RUN mkdir -p /etc/supervisor.d

VOLUME /var/log/websockets

COPY ./supervisord.conf /etc/supervisord.conf
COPY ./websockets.conf /etc/supervisor.d/websockets.conf

EXPOSE 6001

CMD ["/usr/bin/supervisord", "-n", "-c",  "/etc/supervisord.conf"]
