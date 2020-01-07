FROM rabbitmq:latest

# Download additional plugins 
ADD https://bintray.com/rabbitmq/community-plugins/download_file?file_path=rabbitmq_delayed_message_exchange-0.0.1.ez \ 
    /plugins/rabbitmq_delayed_message_exchange.ez
RUN chmod a+r /plugins/rabbitmq_delayed_message_exchange.ez

# Enable additional plugins
RUN set -x \
    && rabbitmq-plugins enable --offline rabbitmq_management \
									     rabbitmq_management_visualiser \
									     rabbitmq_shovel \
									     rabbitmq_shovel_management \
									     rabbitmq_delayed_message_exchange


# Set a new mnesia location for separating it from .erlang.cookie 
# (on Windows .erlang.cookie can not be shared)
ENV RABBITMQ_MNESIA_BASE /data
RUN    mkdir -p /data \
    && chown -R rabbitmq:rabbitmq /data \
	&& chmod -R 777 /data
VOLUME /data

# Set node name for persistent data
ENV RABBITMQ_NODENAME rabbit@localhost

EXPOSE 15671 15672

