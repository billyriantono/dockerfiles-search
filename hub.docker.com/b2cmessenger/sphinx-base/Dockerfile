FROM debian:jessie

RUN echo "deb http://ftp.debian.org/debian jessie-backports main" >> /etc/apt/sources.list \
	&& apt-get update \
	&& DEBIAN_FRONTEND=noninteractive \
	&& apt-get install -y \
        sphinxsearch \
        supervisor \
        cron \
        mysql-client \
    && rm -rf /var/lib/apt/lists/* \
	&& echo 'START=yes' > /etc/default/sphinxsearch \
	&& mkdir -p /var/lib/sphinxsearch/data

COPY conf/en.pak /en.pak
COPY searchd.sh /searchd.sh
COPY indexer.sh /indexer.sh
COPY supervisord.conf /etc/supervisor/supervisord.conf
COPY rest.py /rest.py
COPY docker-entrypoint.sh /docker-entrypoint.sh
COPY dict_to_db.sh /dict_to_db.sh

RUN chmod +x /searchd.sh \
	&& chmod +x /indexer.sh \
	&& chmod +x /rest.py \
	&& chmod +x /docker-entrypoint.sh

ENTRYPOINT ["/docker-entrypoint.sh"]

CMD  /searchd.sh
