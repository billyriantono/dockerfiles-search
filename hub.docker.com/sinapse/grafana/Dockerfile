FROM grafana/grafana:5.2.1

USER root

COPY ./grafana/datasources /etc/grafana/datasources
COPY ./grafana/dashboards /etc/grafana/dashboards
COPY ./grafana/alert-notifications /etc/grafana/alert-notifications
COPY ./grafana/setup.sh /setup.sh
COPY ./grafana.ini /etc/grafana/grafana.ini
COPY ./ldap.toml /etc/grafana/ldap.toml

RUN chmod +x /setup.sh

ENTRYPOINT ["/setup.sh"]
