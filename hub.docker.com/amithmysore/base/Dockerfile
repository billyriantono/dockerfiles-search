FROM phusion/baseimage

ENV HOME /root

CMD ["/sbin/my_init"]

RUN apt-get update && apt-get install -y python ssh curl vim libcurl4-openssl-dev libapr1-dev libaprutil1-dev libapr1-dev libaprutil1 telnet memcached htop libaio1 patch gawk g++ make patch libreadline6-dev libxml2 libxml2-dev libyaml-dev sqlite3 autoconf libgdbm-dev libncurses5-dev automake libtool bison libffi-dev libmagickwand-dev apache2 redis-server --no-install-recommends && apt-get clean && mkdir -p /var/run/sshd && rm -rf /var/lib/apt/lists/*


