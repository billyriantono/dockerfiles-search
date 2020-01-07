FROM guilhem/rabbitmq:plugins

ENV AUTOCLUSTER_VERSION 0.4.1

ADD https://github.com/aweber/rabbitmq-autocluster/releases/download/$AUTOCLUSTER_VERSION/autocluster-$AUTOCLUSTER_VERSION.ez /plugins/
RUN chmod 644 /plugins/autocluster-$AUTOCLUSTER_VERSION.ez

RUN rabbitmq-plugins enable --offline autocluster
