FROM rabbitmq:3.6.10
RUN apt-get update && apt-get install -y wget

# prometheus exporter plugin
ADD ["https://github.com/deadtrickster/prometheus_rabbitmq_exporter/releases/download/rabbitmq-3.6.9.1/accept-0.3.0.ez", \
     "https://github.com/deadtrickster/prometheus_rabbitmq_exporter/releases/download/rabbitmq-3.6.9.1/prometheus-3.2.2.ez", \
     "https://github.com/deadtrickster/prometheus_rabbitmq_exporter/releases/download/rabbitmq-3.6.9.1/prometheus_httpd-1.1.1.ez", \
     "https://github.com/deadtrickster/prometheus_rabbitmq_exporter/releases/download/rabbitmq-3.6.9.1/prometheus_process_collector-1.0.2.ez", \
     "https://github.com/deadtrickster/prometheus_rabbitmq_exporter/releases/download/rabbitmq-3.6.9.1/prometheus_rabbitmq_exporter-v3.6.9.1.ez", \
     "/usr/lib/rabbitmq/lib/rabbitmq_server-${RABBITMQ_VERSION}/plugins/"]
RUN chmod a+r /usr/lib/rabbitmq/lib/rabbitmq_server-${RABBITMQ_VERSION}/plugins/prometheus*.ez /usr/lib/rabbitmq/lib/rabbitmq_server-${RABBITMQ_VERSION}/plugins/accept*.ez \
    && rabbitmq-plugins enable --offline prometheus accept prometheus_rabbitmq_exporter prometheus_process_collector prometheus_httpd

ENV DOCKERIZE_VERSION v0.2.0

RUN wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && tar -C /usr/local/bin -xzvf dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz

RUN mkdir /opt/rabbit 
ADD run.sh /opt/rabbit/

RUN chmod a+x /opt/rabbit/run.sh

ENV RABBITMQ_LOGS=- 
ENV RABBITMQ_SASL_LOGS=-
ENV RABBITMQ_CONFIG="[{rabbit, [{loopback_users, []}]}]."
ENV ERLANG_COOKIE=RABBITMQ
ENV WAIT_CLUSTERED_WITH="250s"

VOLUME /var/lib/rabbitmq/mnesia

EXPOSE 5672
EXPOSE 15672
EXPOSE 25672
EXPOSE 4369
EXPOSE 9100
EXPOSE 9101
EXPOSE 9102
EXPOSE 9103
EXPOSE 9104
EXPOSE 9105

CMD /opt/rabbit/run.sh
