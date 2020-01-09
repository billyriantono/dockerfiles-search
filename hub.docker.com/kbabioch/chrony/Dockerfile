FROM fedora:latest
LABEL MAINTAINER Karol Babioch <karol@babioch.de>
RUN dnf -y install --nodocs chrony && \
  dnf -y clean all
EXPOSE 123/udp
#ENV CHRONY_HWTIMESTAMP=0
COPY chrony.conf /etc/chrony.conf
COPY entrypoint.sh /
ENTRYPOINT ["/entrypoint.sh"]
COPY healthcheck.sh /
HEALTHCHECK CMD "/healthcheck.sh"
