# vim: set ft=dockerfile:
FROM ubuntu:16.04
MAINTAINER Cat Plus Plus <piotrlegnica@piotrl.pl>

ENV UNPRIV_USER=unpriv

ADD . /build
RUN sync && bash /build/provision.sh && sync && rm -rf /build

WORKDIR /tmp
ENTRYPOINT ["/entry/point"]
CMD ["bash"]
