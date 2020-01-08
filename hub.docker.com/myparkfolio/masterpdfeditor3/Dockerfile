FROM ubuntu:14.04

WORKDIR /

RUN  cd /tmp \
  && apt-get install -y wget libqt4-svg libqt4-network libqtcore4 libqtgui4 \
  && wget http://code-industry.net/public/master-pdf-editor_2.2.05_amd64.deb \
  && dpkg -i master-pdf-editor_2.2.05_amd64.deb \
  && rm master-pdf-editor_2.2.05_amd64.deb

ENV HOME /home/developer
ENV UID 1000
ENV GID 1000

COPY docker-entrypoint.sh /

RUN chmod a+x /docker-entrypoint.sh

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["/usr/bin/masterpdfeditor3"]
