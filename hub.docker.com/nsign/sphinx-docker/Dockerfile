FROM debian:stable

RUN apt-get update && apt-get install --yes --no-install-recommends sphinxsearch

RUN apt-get autoremove --yes && apt-get clean all

COPY sphinx.conf /etc/sphinxsearch/sphinx.conf

ADD start.sh /
RUN chmod +x /start.sh

CMD ["/start.sh"]
