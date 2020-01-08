FROM docker.elastic.co/elasticsearch/elasticsearch:5.2.1

LABEL maintainer="Franck Coutouly <towl.fr@gmail.com>"

RUN elasticsearch-plugin install analysis-phonetic

COPY ./conf/ /usr/share/elasticsearch/config/
