FROM mariadb:10.1-bionic

RUN apt-get update \
 && apt-get install -y --no-install-recommends --no-install-suggests \
      curl \
      netcat \
      pigz \
      percona-toolkit \
      percona-xtrabackup \
      pv
      
# Download qpress.tar doesn't work
#RUN curl -sSL -o /tmp/qpress.tar http://www.quicklz.com/qpress-11-linux-x64.tar \
# && tar -C /usr/local/bin -xf /tmp/qpress.tar qpress \
# && chmod +x /usr/local/bin/qpress
RUN curl -sSL -o /tmp/qpress_11-1.bionic_amd64.deb https://downloads.mariadb.com/Tools/debian/pool/main/q/qpress/qpress_11-1.bionic_amd64.deb \
 && dpkg -i /tmp/qpress_11-1.bionic_amd64.deb \
 && rm /tmp/qpress_11-1.bionic_amd64.deb

# copy local files
COPY root/ /

# Fix permissions
RUN chown -R mysql:mysql /etc/mysql \
 && chmod -R go-w /etc/mysql
 
# Cleanup
RUN apt-get clean \
 && rm -rf /tmp/* /var/cache/apk/* /var/lib/apt/lists/*

EXPOSE 3306 4444 4567 4567/udp 4568 8080 8081

HEALTHCHECK CMD /usr/local/bin/healthcheck.sh
ENV SST_METHOD=xtrabackup-v2

ENTRYPOINT ["start.sh"]
