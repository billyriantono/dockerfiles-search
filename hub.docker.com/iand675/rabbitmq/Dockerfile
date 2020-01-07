FROM ubuntu
MAINTAINER Ian Duncan <ian@iankduncan.com>
ADD http://www.rabbitmq.com/releases/rabbitmq-server/v3.2.1/rabbitmq-server_3.2.1-1_all.deb /tmp/rabbit.deb
RUN apt-get update
RUN dpkg-divert --local --rename --add /sbin/initctl
RUN ln -s /bin/true /sbin/initctl
RUN apt-get install -y logrotate erlang-nox
RUN dpkg -i /tmp/rabbit.deb
RUN rm /tmp/rabbit.deb
RUN rabbitmq-plugins enable rabbitmq_management
EXPOSE 5672 15672
CMD /usr/sbin/rabbitmq-server
VOLUME ["/var/lib/rabbitmq/mnesia", "/var/log/rabbitmq"]
