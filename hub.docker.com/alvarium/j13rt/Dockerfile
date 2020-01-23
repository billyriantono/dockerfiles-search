FROM fedora

LABEL maintainer="Luiz Fernando Pereira <luizfernandopereira@outlook.com.br>"

RUN dnf install 389-ds-base -y && \
    dnf clean all && \
    mkdir -p /data/config && \
    mkdir -p /data/ssca && \
    mkdir -p /data/run  && \
    ln -s /data/ssca /etc/dirsrv/ssca && \
    ln -s /data/run /var/run/dirsrv

COPY dscontainer.py /usr/sbin/dscontainer
RUN chmod +x /usr/sbin/dscontainer
EXPOSE 389 636
VOLUME /data
CMD [ "/usr/sbin/dscontainer", "-r" ]