FROM logstash:2.0.0-1

RUN plugin install --no-verify logstash-filter-environment

CMD ["logstash", "agent"]
