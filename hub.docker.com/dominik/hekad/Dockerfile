# dominik/hekad
#
# BUILD: docker build --no-cache --rm -t dominik/hekad .
# RUN:   docker run dominik/hekad

FROM ubuntu:14.04
MAINTAINER Dominik Tobschall <dominik@fruux.com>

RUN apt-get update && apt-get install -y \
    wget

RUN wget -P /tmp https://github.com/mozilla-services/heka/releases/download/v0.5.2/heka_0.5.2_amd64.deb
RUN dpkg -i /tmp/heka_0.5.2_amd64.deb
RUN rm /tmp/heka_0.5.2_amd64.deb

ENTRYPOINT ["hekad"]
CMD ["-help"]
