FROM teodorescuserban/hdx-base-ckan:latest

MAINTAINER Serban Teodorescu, teodorescu.serban@gmail.com

RUN apt-get -qq update && \
    apt-get install -qq -y python3-requests mysql-client-5.5 && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    /etc/my_init.d/00_regen_ssh_host_keys.sh && \
    git clone https://github.com/OCHA-DAP/hdx-tools.git /srv/tools && \
    ln -s /srv/tools/hdxckantool.py /usr/bin/hdxckantool && \
    ln -s /srv/tools/hdxcpstool.py /usr/bin/hdxcpstool && \
    ln -s /srv/tools/hdxblogtool.sh /usr/bin/hdxblogtool && \
    ln -s /srv/tools/uploadScrapers.py /usr/bin/uploadScrapers

VOLUME ["/srv/backup", "/srv/files", "/srv/logs"]

CMD ["/sbin/my_init"]
