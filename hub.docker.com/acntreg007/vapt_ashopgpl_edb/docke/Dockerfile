FROM rabbitmq:3
ENV APT_LISTCHANGES_FRONTEND mail
ENV DEBIAN_FRONTEND noninteractive
RUN /usr/sbin/rabbitmq-plugins enable --offline rabbitmq_management
RUN mkdir -p /usr/lib/rabbitmq/plugins && apt-get update && apt-get install -yq wget && \
    wget -O /usr/lib/rabbitmq/plugins/rabbitmq_delayed_message_exchange.ez \
    "https://bintray.com/rabbitmq/community-plugins/download_file?file_path=rabbitmq_delayed_message_exchange-0.0.1.ez"
RUN /usr/sbin/rabbitmq-plugins enable --offline rabbitmq_delayed_message_exchange
EXPOSE 15671 15672
