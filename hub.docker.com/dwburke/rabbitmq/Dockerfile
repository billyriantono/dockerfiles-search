FROM dwburke/erlang
MAINTAINER Dan Burke <dburke@addictmud.org>
RUN echo 'deb http://www.rabbitmq.com/debian/ testing main' | tee /etc/apt/sources.list.d/rabbitmq.list
RUN wget -O- https://www.rabbitmq.com/rabbitmq-release-signing-key.asc | apt-key add -
RUN apt-get update && apt-get install -y rabbitmq-server && apt-get clean
RUN echo "[{rabbit,[{loopback_users,[]}]}]." > /etc/rabbitmq/rabbitmq.config
EXPOSE 5672 15672 25672 4369
RUN rm -f /.erlang.cookie
RUN rm -rf /var/lib/rabbitmq/mnesia
ADD start_server.sh /
CMD /start_server.sh
