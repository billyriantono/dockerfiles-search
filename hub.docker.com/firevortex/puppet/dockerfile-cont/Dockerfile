FROM kibana:4.4.2

RUN apt-get update && apt-get install -y netcat

COPY entrypoint.sh /tmp/entrypoint.sh
RUN chmod +x /tmp/entrypoint.sh

RUN kibana plugin --install elastic/sense
RUN kibana plugin --install kibana/timelion

CMD ["/tmp/entrypoint.sh"]
