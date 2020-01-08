FROM python:3.7

RUN mkdir -p /root/.config /config
RUN ln -s /config /root/.config/gphotos-sync 
VOLUME /config

RUN mkdir /target
VOLUME /target

RUN pip install gphotos-sync

ENTRYPOINT [ "gphotos-sync" ]

