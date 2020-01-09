FROM telegraf:1.9

RUN apt-get update
RUN apt-get install -y libnet-ssh2-perl

RUN curl -L https://github.com/centreon/centreon-plugins/archive/20181031.tar.gz -o /tmp/centreon-plugins.tar.gz
RUN tar xzf /tmp/centreon-plugins.tar.gz -C /opt
RUN rm -f /tmp/centreon-plugins.tar.gz
