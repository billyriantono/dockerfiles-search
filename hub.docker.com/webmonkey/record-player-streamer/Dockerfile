FROM arm32v6/alpine
RUN apk add icecast darkice supervisor
COPY darkice.cfg /etc/darkice.cfg
COPY supervisord-*.ini /etc/supervisor.d/
CMD /usr/bin/supervisord --configuration /etc/supervisord.conf --nodaemon
