FROM teodorescuserban/hdx-base-email:latest

MAINTAINER Serban Teodorescu, teodorescu.serban@gmail.com


RUN curl -sLo dropbox.tar.gz "https://www.dropbox.com/download?plat=lnx.x86_64" && \
    tar xvzf dropbox.tar.gz && \
    curl -sLo /srv/dropbox.py "https://www.dropbox.com/download?dl=packages/dropbox.py" && \
    chmod +x /srv/dropbox.py && \
    ln -s /srv/dropbox.py /usr/bin/dropbox.py && \
    mkdir -p /etc/service/dropbox && \
    touch /etc/service/dropbox/down

ADD run /etc/service/dropbox/run
RUN chmod u+x /etc/service/dropbox/run

RUN /etc/my_init.d/00_regen_ssh_host_keys.sh
CMD ["/sbin/my_init"]
