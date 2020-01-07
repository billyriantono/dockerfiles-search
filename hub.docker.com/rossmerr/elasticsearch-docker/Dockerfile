FROM elasticsearch:1.5.2

WORKDIR /usr/share/elasticsearch/bin/

# install the head plugin
RUN plugin -install mobz/elasticsearch-head

# install the inquisitor plugin
RUN plugin -install polyfractal/elasticsearch-inquisitor

WORKDIR /

CMD ["elasticsearch"]