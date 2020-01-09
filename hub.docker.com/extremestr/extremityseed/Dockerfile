# Docker container with utorrent
FROM ubuntu:trusty
MAINTAINER test

RUN locale-gen en_US.UTF-8
ENV LC_ALL en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en

#
# Create user and group for utorrent
#
RUN useradd -G users -m utorrent
RUN apt-get update && \
		apt-get install -y --no-install-recommends vsftpd db-util && \
		apt-get clean
#
# Add utorrent dist
#
ADD http://download.ap.bittorrent.com/track/beta/endpoint/utserver/os/linux-x64-ubuntu-13-04 /tmp/utserver.tar.gz

#
# Add utorrent init script and config.
#
ADD utserver.sh /opt/utorrent/utserver.sh
ADD utserver.conf /opt/utorrent/utserver.conf

ENV FTP_USER admin
ENV FTP_PASS admin
ENV PASV_ADDRESS REQUIRED

COPY vsftpd.conf /etc/vsftpd/
COPY vsftpd_virtual /etc/pam.d/
COPY run-vsftpd.sh /usr/sbin/

RUN chmod +x /usr/sbin/run-vsftpd.sh && \
		mkdir -p /var/run/vsftpd/empty

#
# Unpack utorrent and change permissions
#
VOLUME ["/utorrent", "/data"]
EXPOSE 8080 6881 20 21

RUN tar vxzf /tmp/utserver.tar.gz --strip-components 1 -C /opt/utorrent && \
    rm -f /tmp/utserver.tar.gz && \
    chown -R utorrent:utorrent /utorrent && \
    chmod 755 /opt/utorrent/utserver.sh

#
# Start utorrent.
#

WORKDIR /utorrent
USER utorrent

CMD ["/opt/utorrent/utserver.sh"]
CMD ["/usr/sbin/run-vsftpd.sh"]
