FROM logstash:1.5.6-1

RUN plugin install logstash-input-http_poller

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["-e", ""]