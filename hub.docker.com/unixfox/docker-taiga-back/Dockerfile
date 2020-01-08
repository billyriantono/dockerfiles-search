FROM dockertaiga/back

WORKDIR /srv/taiga

## Install Slack extension
RUN LC_ALL=C pip install --no-cache-dir taiga-contrib-slack

EXPOSE 80

WORKDIR /srv/taiga/back

VOLUME ["/taiga-conf", "/taiga-media"]

CMD ["/start.sh"]