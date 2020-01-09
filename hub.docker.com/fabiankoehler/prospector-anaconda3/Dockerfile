# -*- docker-image-name: "prospector-anaconda3" -*-
FROM continuumio/anaconda3
LABEL maintainer="fkoehler1024@googlemail.com"

# install prospector
RUN pip install "prospector[with_everything]==1.1.4"
ENTRYPOINT ["/usr/bin/prospector"]
