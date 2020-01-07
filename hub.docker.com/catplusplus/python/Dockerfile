# vim: set ft=dockerfile:
FROM catplusplus/base
MAINTAINER Cat Plus Plus <piotrlegnica@piotrl.pl>

ADD . /build
RUN sync && bash /build/provision.sh && sync && rm -rf /build
