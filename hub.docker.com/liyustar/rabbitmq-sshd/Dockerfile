FROM liyustar/sshd
MAINTAINER liyustar <liyustar@gmail.com>

# RUN echo 'deb http://www.rabbitmq.com/debian/ stable main' | tee /etc/apt/sources.list.d/rabbitmq.list
# ADD ./rabbitmq-signing-key-public.asc ${work}
# RUN apt-key add rabbitmq-signing-key-public.asc

RUN apt-get update
RUN apt-get install -y rabbitmq-server

# enable rabbitmq plugins
RUN rabbitmq-plugins enable rabbitmq_management

# rabbitmq-server config
ADD erlang.cookie /var/lib/rabbitmq/.erlang.cookie
RUN chown rabbitmq:rabbitmq /var/lib/rabbitmq/.erlang.cookie
RUN chmod 400 /var/lib/rabbitmq/.erlang.cookie

RUN mkdir -p /opt/rabbit
ADD startrabbit.sh /opt/rabbit/startrabbit.sh

# Declare
EXPOSE 15672
EXPOSE 5672
EXPOSE 22

CMD ["/opt/rabbit/startrabbit.sh"]
