FROM elasticsearch:5.5
MAINTAINER "Talos Digital"

RUN elasticsearch-plugin install analysis-phonetic
RUN elasticsearch-plugin install analysis-icu

EXPOSE 9200 9300
ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["elasticsearch"]
