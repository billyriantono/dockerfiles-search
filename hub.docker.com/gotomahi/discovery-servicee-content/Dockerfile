# BBUild an image that will run the results xrootd server

FROM cloudpg/cachingondemand:v4.8.3

WORKDIR /usr/src/app
COPY etc/xrootd-results.cfg /etc/xrootd/xrootd-results.cfg
RUN chown -R xrootd:xrootd /etc/xrootd

RUN mkdir -p /data/xrd
RUN chown -R xrootd:xrootd /data/xrd

ENTRYPOINT [ "/bin/bash", "-c", "chown -R xrootd:xrootd /data/xrd; sudo -u xrootd xrootd -c /etc/xrootd/xrootd-results.cfg" ]
