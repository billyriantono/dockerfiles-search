FROM grafana/grafana:4.6.1

ADD conf.d /etc/grafana/

ENV GF_SERVER_ROOT_URL="https://grafana.srv.cat"

EXPOSE 3000

ENTRYPOINT ["/run.sh"]
