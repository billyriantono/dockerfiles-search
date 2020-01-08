FROM docker
RUN apk --no-cache add bash

ENV HOST jptest03.mvista.com 
ENV BUILDER_IMAGE jpuhlman/koji-builder
ENV KOJI_SCMS gitcentos.mvista.com:/centos/upstream/packages/*:common:/chroot_tmpdir/scmroot/common/get_sources.sh
ENV KOJI_MOCK /koji/mock

RUN mkdir -p /var/lib/mock
COPY entrypoint.sh /
RUN chmod +x /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
