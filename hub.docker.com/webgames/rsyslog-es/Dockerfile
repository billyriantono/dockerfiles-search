FROM      ubuntu:trusty

# Install rsyslog and rsyslog-elasticsearch extensions. All in one
# go to reduce amount of layers.
RUN       apt-get -y update && \
          apt-get upgrade -y --no-install-recommends && \
          apt-get install -y --no-install-recommends \
          python-software-properties software-properties-common && \
          sudo add-apt-repository ppa:adiscon/v8-stable && \
          apt-get -y update && \
          apt-get -q -y --no-install-recommends install \
          rsyslog rsyslog-elasticsearch && \
          apt-get clean && \
          rm -rf /var/lib/apt/lists/*

COPY      entrypoint.sh                  /
COPY	  rsyslog.conf                   /etc/
COPY      rsyslog_elasticsearch.conf     /etc/rsyslog.d/
# bugfix ubuntu 14 https://bugs.launchpad.net/ubuntu/+source/logrotate/+bug/1644996
RUN 	  sed -i 's/^su root syslog/su root adm/' /etc/logrotate.conf
ENTRYPOINT ["/entrypoint.sh"]
CMD ["-n"]
